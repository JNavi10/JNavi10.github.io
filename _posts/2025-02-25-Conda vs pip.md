# Conda vs pip

# **What are they?**

Conda is a package and environment manager that handles both Python and system dependencies.

pip is Python’s standard package manager, installing only Python packages from PyPI.

# **How are they different?**

- Conda manages system dependencies; pip does not.
- Conda prevents dependency conflicts before installing; pip resolves dependencies individually for each package, which can cause conflicts.
- Conda is heavier because it installs more than just Python packages.

# **Anaconda vs. Miniconda**

- **Anaconda** is a full Python distribution that includes Conda, pre-installed data science libraries, and a package manager. It is large (~3GB).
- **Miniconda** is a minimal version of Anaconda that includes only Conda and Python. It is much smaller (~500MB).

# **What should you use?**

- **Use Miniconda venv** for everyday development.
    - Keeps your system clean by avoiding global Python installs.
    - Avoids dependency conflicts, which are inevitable as projects grow.
    - Lighter than Anaconda.
    - Install packages with Conda first; if not supported, use pip.
- **Use pip in embedded systems** where space is limited.

# **Glossary**

Note: These terms are explained in a way that I understand them. They may deviate from official definitions. For official definitions, refer to the official Python glossary.

[Glossary](https://docs.python.org/3/glossary.html)

### **Package**

A directory that organizes Python modules and/or sub-packages.

### **Module**

A single Python file containing reusable code.

### **Virtual Environment (venv)**

An isolated Python environment that keeps dependencies separate from the system Python.

### **Dependency**

A package required by another package to function correctly.

### **System Dependency**

A non-Python library (e.g., `libjpeg`, `ffmpeg`) that certain Python packages need to work.

### **Dependency Conflict**

A situation where two or more packages require incompatible versions of the same dependency.