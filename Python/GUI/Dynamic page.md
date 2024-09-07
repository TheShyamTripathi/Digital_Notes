Yes, it's possible to dynamically change the content of input and output frames in Tkinter based on the functions you call. You can clear the existing widgets in the frames and add new widgets as needed. This is useful when you want to display different forms or output areas on the same page.

Here's an example where two pages dynamically change their content:

### Example: Dynamic Page Content in Tkinter

```python
import tkinter as tk
from tkinter import messagebox
import pymysql

def connect_db():
    try:
        con = pymysql.connect(host="localhost", user="root", password="Shyamsql@123", database="Skyway_Flight")
        return con
    except pymysql.Error as e:
        messagebox.showerror("Database Connection Error", f"Error: {e}")
        return None

def clear_frame(frame):
    for widget in frame.winfo_children():
        widget.destroy()

def page1():
    clear_frame(input_frame)
    clear_frame(output_frame)

    # Add input fields for Page 1
    tk.Label(input_frame, text="Enter Plane ID:").grid(row=0, column=0)
    plane_id_entry = tk.Entry(input_frame)
    plane_id_entry.grid(row=0, column=1)

    tk.Button(input_frame, text="Search Plane", command=lambda: fetch_plane_info(plane_id_entry.get())).grid(row=1, column=0, columnspan=2)

def fetch_plane_info(plane_id):
    clear_frame(output_frame)

    con = connect_db()
    if not con:
        return
    
    try:
        cur = con.cursor()
        query = "SELECT * FROM plane_info WHERE Plane_ID=%s"
        cur.execute(query, (plane_id,))
        plane_info = cur.fetchone()

        if plane_info:
            headers = ["Plane ID", "Model", "Total Seats", "Year Manufactured"]
            for col, header in enumerate(headers):
                tk.Label(output_frame, text=header, borderwidth=2, relief="groove").grid(row=0, column=col, sticky="nsew")
            
            for col, data in enumerate(plane_info):
                tk.Label(output_frame, text=data, borderwidth=2, relief="groove").grid(row=1, column=col, sticky="nsew")
        else:
            tk.Label(output_frame, text="No plane information found for this ID.").grid(row=0, column=0)

    except pymysql.Error as e:
        messagebox.showerror("Error", f"Error: {e}")
    finally:
        if con:
            con.close()

def page2():
    clear_frame(input_frame)
    clear_frame(output_frame)

    # Add input fields for Page 2
    tk.Label(input_frame, text="Enter Flight Number:").grid(row=0, column=0)
    flight_no_entry = tk.Entry(input_frame)
    flight_no_entry.grid(row=0, column=1)

    tk.Button(input_frame, text="Search Flight", command=lambda: fetch_flight_info(flight_no_entry.get())).grid(row=1, column=0, columnspan=2)

def fetch_flight_info(flight_no):
    clear_frame(output_frame)

    con = connect_db()
    if not con:
        return
    
    try:
        cur = con.cursor()
        query = "SELECT * FROM flight_info WHERE Flight_NO=%s"
        cur.execute(query, (flight_no,))
        flight_info = cur.fetchone()

        if flight_info:
            headers = ["Flight No", "Start", "Destination", "Fare", "Available Seats", "Date", "Plane ID"]
            for col, header in enumerate(headers):
                tk.Label(output_frame, text=header, borderwidth=2, relief="groove").grid(row=0, column=col, sticky="nsew")
            
            for col, data in enumerate(flight_info):
                tk.Label(output_frame, text=data, borderwidth=2, relief="groove").grid(row=1, column=col, sticky="nsew")
        else:
            tk.Label(output_frame, text="No flight information found for this number.").grid(row=0, column=0)

    except pymysql.Error as e:
        messagebox.showerror("Error", f"Error: {e}")
    finally:
        if con:
            con.close()

# Example GUI Setup
root = tk.Tk()
root.title("Flight Management System")

# Input Frame
input_frame = tk.Frame(root, bd=2, relief=tk.SUNKEN, padx=10, pady=10)
input_frame.grid(row=0, column=0, padx=10, pady=10)

# Output Frame
output_frame = tk.Frame(root, bd=2, relief=tk.SUNKEN, padx=10, pady=10)
output_frame.grid(row=1, column=0, padx=10, pady=10)

# Menu or Navigation to Switch Between Pages
menu_frame = tk.Frame(root)
menu_frame.grid(row=2, column=0, padx=10, pady=10)

tk.Button(menu_frame, text="Go to Page 1", command=page1).grid(row=0, column=0)
tk.Button(menu_frame, text="Go to Page 2", command=page2).grid(row=0, column=1)

# Initialize the first page
page1()

# Run the GUI main loop
root.mainloop()
```

### Explanation:
1. **Dynamic Content with `clear_frame()`**: The `clear_frame()` function is used to remove all widgets from a frame. When switching between pages, this function is called to clear the input and output frames, allowing you to populate them with new widgets for the current page.

2. **Page 1 (`page1()`)**: This page allows the user to enter a Plane ID and search for information related to that plane. The function `fetch_plane_info()` is called to fetch and display the data.

3. **Page 2 (`page2()`)**: This page allows the user to enter a Flight Number and search for information related to that flight. The function `fetch_flight_info()` is called to fetch and display the data.

4. **Menu/Navigation**: A simple menu with two buttons is provided at the bottom to switch between Page 1 and Page 2.

5. **Automatic Update**: Each page automatically clears and updates the content based on the user’s selection, showing the relevant input fields and data.

### Result:
When you switch between the two pages, the input and output frames will automatically clear and display new content according to the functions you call. This way, you can dynamically update the interface without creating new windows or requiring additional user actions beyond selecting the page.

This method is flexible and can be expanded to include additional pages or more complex input/output structures.
