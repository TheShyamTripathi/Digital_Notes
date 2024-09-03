Here's an example of a basic Tkinter application that demonstrates how to create multiple window pages with navigation buttons to move between them, including a button to return to the homepage (main page):

```python
import tkinter as tk

class App(tk.Tk):
    def __init__(self):
        super().__init__()
        self.title("Multiple Window Example")
        self.geometry("400x300")

        # Create frames for different pages
        self.home_page = HomePage(self)
        self.page_one = PageOne(self)
        self.page_two = PageTwo(self)

        # Show the home page initially
        self.show_frame(self.home_page)

    def show_frame(self, frame):
        frame.tkraise()

class HomePage(tk.Frame):
    def __init__(self, master):
        tk.Frame.__init__(self, master)
        self.grid(row=0, column=0, sticky="nsew")

        label = tk.Label(self, text="Home Page", font=("Helvetica", 18))
        label.pack(pady=10)

        page_one_button = tk.Button(self, text="Go to Page One",
                                    command=lambda: master.show_frame(master.page_one))
        page_one_button.pack(pady=5)

        page_two_button = tk.Button(self, text="Go to Page Two",
                                    command=lambda: master.show_frame(master.page_two))
        page_two_button.pack(pady=5)

class PageOne(tk.Frame):
    def __init__(self, master):
        tk.Frame.__init__(self, master)
        self.grid(row=0, column=0, sticky="nsew")

        label = tk.Label(self, text="Page One", font=("Helvetica", 18))
        label.pack(pady=10)

        home_button = tk.Button(self, text="Go to Home Page",
                                command=lambda: master.show_frame(master.home_page))
        home_button.pack(pady=5)

        next_page_button = tk.Button(self, text="Go to Page Two",
                                     command=lambda: master.show_frame(master.page_two))
        next_page_button.pack(pady=5)

class PageTwo(tk.Frame):
    def __init__(self, master):
        tk.Frame.__init__(self, master)
        self.grid(row=0, column=0, sticky="nsew")

        label = tk.Label(self, text="Page Two", font=("Helvetica", 18))
        label.pack(pady=10)

        home_button = tk.Button(self, text="Go to Home Page",
                                command=lambda: master.show_frame(master.home_page))
        home_button.pack(pady=5)

        prev_page_button = tk.Button(self, text="Go to Page One",
                                     command=lambda: master.show_frame(master.page_one))
        prev_page_button.pack(pady=5)

if __name__ == "__main__":
    app = App()
    app.mainloop()
```

### Explanation:
1. **`App` Class:** This is the main application class inheriting from `tk.Tk`. It initializes the main window and sets up frames (pages).
2. **`HomePage`, `PageOne`, `PageTwo` Classes:** These classes define the layout and widgets for each page. Each page is a `tk.Frame`.
3. **Navigation:** 
   - Buttons in each page call the `show_frame` method from the `App` class, which raises the selected frame to the top, effectively switching the displayed page.
   - The "Home Page" button on each page returns the user to the homepage.
   - The "Next" and "Previous" buttons allow navigating between pages.

### Usage:
- **Home Page:** Buttons to navigate to Page One and Page Two.
- **Page One:** Buttons to go back to Home Page and forward to Page Two.
- **Page Two:** Buttons to return to Home Page and go back to Page One.

You can run this code in your Python environment to see the functionality.
