In **Tkinter**, the graphical user interface (GUI) updates after the event loop processes all pending tasks, which typically happens once your function returns. Therefore, if a function contains time-consuming tasks, it can block the GUI from updating, making it appear unresponsive and slow.

To solve this, you can split the work into two parts:

    1. Run the fast part.
    2. Run the slow part in separate thread, so the function returns and GUI can update.

To achieve this, you can use Python's **threading** library.



```python
import tkinter as tk
import threading
import time

def long_running_task():
    # Slow part
    time.sleep(3)  # Simulate a long-running task
    label.config(text="Slow part done!")
    print("Slow Task done!")

def run_function():
    # Fast part
    label.config(text="Fast part done!")

    # Run the slow part in a separate thread
    threading.Thread(target=long_running_task).start()

    # Function returns before slow part finishes
    print("Function Returned")

# Set up the GUI
root = tk.Tk()

label = tk.Label(root, text="Starting...")
label.pack(pady=20)

button = tk.Button(root, text="Run Function", command=run_function)
button.pack(pady=20)


# Run the GUI
root.mainloop()

```

    Function Returned
    Slow Task done!
    

From the results above, we can cleary see that the function returned first and the slow part executedly separately from the function.

