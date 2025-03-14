# Debugging SQLAlchemy Duplicate Insertion Issue

## What Happened?

While building a **Pixiv scraper** using **SQLAlchemy + PostgreSQL**, I encountered a bizarre issue:

- The **first script run allowed duplicate inserts**, despite `artist_id` being a **primary key**.
- **Subsequent runs correctly enforced** the constraint.
- For the first run, `while True` loop kept inserting **without ever triggering an error**.

## The Real Cause: **SQLAlchemy Session Caching**

SQLAlchemy sessions **do not reflect real-time database changes**. Instead, they:

- **Uses its own in-memory representation of the database**, so committed changes are invisible to the session until explicitly refreshed.

This explains why:

- The first script run allowed two inserts before PostgreSQL checked for duplicates.
- Subsequent runs, which started with a fresh session, correctly detected the existing row.

## The Fix: Use a Persistent Connection (`self.con`)

To bypass session caching, I switched from **SQLAlchemy ORM sessions** to a **direct database connection**:

```python
from sqlalchemy import create_engine, text, exc

class DBManager:
    def __init__(self):
        self.engine = create_engine("postgresql://user:password@localhost:5432/database_name", isolation_level="AUTOCOMMIT")
        self.con = self.engine.connect()

    def safe_insert(self, artist_id, artist_name, is_following):
        try:
            self.con.execute(
                text("INSERT INTO artist (artist_id, artist_name, is_following) VALUES (:id, :name, :follow)"),
                {"id": artist_id, "name": artist_name, "follow": is_following}
            )
            print("INSERT successful")
        except exc.IntegrityError:
            raise ValueError("Duplicate entry: Record already exists")
        except exc.SQLAlchemyError as e:
            raise Exception(f"SQL ERROR: {e}")

    def remove_artist(self, artist_id):
        try:
            result = self.con.execute(text("DELETE FROM artist WHERE artist_id = :id"), {"id": artist_id})
            if result.rowcount == 0:
                raise ValueError(f"Artist {artist_id} does not exist.")
        except exc.SQLAlchemyError as e:
            raise Exception(f"SQL ERROR: {e}")

```

## Why This Works

- **No session caching** → Every query interacts directly with the database.
- **Immediate constraint enforcement** → Inserts fail **immediately** on duplicates.

## Conclusion

SQLAlchemy sessions can **hide real-time database updates** due to caching and delayed constraint enforcement. For real-time behavior:

- **Use direct DB connections (`self.con`)** instead of ORM sessions.
- **Only use sessions when batch transactions are needed.**