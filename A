import tkinter as tk
from tkinter import messagebox

# Define the Task class
class Task:
    def __init__(self, title, category, priority):
        self.title = title
        self.category = category
        self.priority = priority

    def __str__(self):
        return f"{self.title} ({self.category}, Priority: {self.priority})"

# Define the ToDoList class
class ToDoList:
    def __init__(self):
        self.tasks = []

    def add_task(self, task):
        self.tasks.append(task)

    def remove_task(self, task_title):
        for task in self.tasks:
            if task.title == task_title:
                self.tasks.remove(task)
                return True
        return False

    def get_all_tasks(self):
        return self.tasks

    def get_tasks_by_category(self, category):
        return [task for task in self.tasks if task.category == category]

# Define the main application window
class ToDoApp:
    def __init__(self, root):
        self.root = root
        self.root.title("To-Do List Application")
        self.todo_list = ToDoList()
        self.categories = ["Work", "Personal", "Study", "Miscellaneous"]

        # Add Task Section
        tk.Label(root, text="Add New Task").grid(row=0, column=0, columnspan=2, pady=10)
        tk.Label(root, text="Title:").grid(row=1, column=0, sticky="e")
        tk.Label(root, text="Category:").grid(row=2, column=0, sticky="e")
        tk.Label(root, text="Priority:").grid(row=3, column=0, sticky="e")

        self.title_entry = tk.Entry(root)
        self.title_entry.grid(row=1, column=1)
        
        self.category_var = tk.StringVar(value=self.categories[0])
        tk.OptionMenu(root, self.category_var, *self.categories).grid(row=2, column=1)

        self.priority_var = tk.StringVar(value="Medium")
        tk.OptionMenu(root, self.priority_var, "High", "Medium", "Low").grid(row=3, column=1)

        tk.Button(root, text="Add Task", command=self.add_task).grid(row=4, column=0, columnspan=2, pady=10)

        # Task Display Section
        tk.Label(root, text="Tasks").grid(row=5, column=0, columnspan=2, pady=10)

        self.tasks_listbox = tk.Listbox(root, width=50, height=10)
        self.tasks_listbox.grid(row=6, column=0, columnspan=2)

        tk.Button(root, text="Remove Task", command=self.remove_task).grid(row=7, column=0, columnspan=2, pady=10)

        # Display by Category Section
        tk.Label(root, text="Filter by Category").grid(row=8, column=0, columnspan=2, pady=10)
        self.filter_category_var = tk.StringVar(value=self.categories[0])
        tk.OptionMenu(root, self.filter_category_var, *self.categories).grid(row=9, column=0, columnspan=2)
        tk.Button(root, text="Display by Category", command=self.display_by_category).grid(row=10, column=0, columnspan=2, pady=10)

        # Refresh Display Section
        tk.Button(root, text="Show All Tasks", command=self.display_tasks).grid(row=11, column=0, columnspan=2, pady=10)

    def add_task(self):
        title = self.title_entry.get().strip()
        category = self.category_var.get()
        priority = self.priority_var.get()
        
        if title:
            task = Task(title, category, priority)
            self.todo_list.add_task(task)
            self.display_tasks()
            self.title_entry.delete(0, tk.END)
        else:
            messagebox.showwarning("Input Error", "Task title cannot be empty.")

    def remove_task(self):
        selected_task = self.tasks_listbox.get(tk.ACTIVE)
        if selected_task:
            task_title = selected_task.split(" (")[0]  # Extract the title before the first parenthesis
            if self.todo_list.remove_task(task_title):
                self.display_tasks()
                messagebox.showinfo("Success", f"Removed task: {task_title}")
            else:
                messagebox.showwarning("Error", "Task not found.")
        else:
            messagebox.showwarning("Selection Error", "No task selected.")

    def display_tasks(self):
        self.tasks_listbox.delete(0, tk.END)  # Clear the listbox
        for task in self.todo_list.get_all_tasks():
            self.tasks_listbox.insert(tk.END, str(task))

    def display_by_category(self):
        category = self.filter_category_var.get()
        tasks_in_category = self.todo_list.get_tasks_by_category(category)
        
        self.tasks_listbox.delete(0, tk.END)  # Clear the listbox
        if tasks_in_category:
            for task in tasks_in_category:
                self.tasks_listbox.insert(tk.END, str(task))
        else:
            self.tasks_listbox.insert(tk.END, f"No tasks in the {category} category.")

# Run the application
root = tk.Tk()
app = ToDoApp(root)
root.mainloop()
