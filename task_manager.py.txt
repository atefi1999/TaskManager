class Task:
    def __init__(self, title, description=""):
        self.title = title              # Task title
        self.description = description  # Task description
        self.done = False               # Status (done or not)

    def mark_done(self):
        """Mark task as done"""
        self.done = True

    def edit(self, new_title, new_description=""):
        """Edit task title and description"""
        self.title = new_title
        self.description = new_description

    def __str__(self):
        status = "✔ Done" if self.done else "✘ Pending"
        return f"{self.title} - {self.description} ({status})"


class TaskManager:
    def __init__(self):
        self.tasks = []   # List of tasks

    def add_task(self, title, description=""):
        """Add a new task"""
        task = Task(title, description)
        self.tasks.append(task)

    def delete_task(self, index):
        """Delete a task by index"""
        if 0 <= index < len(self.tasks):
            self.tasks.pop(index)

    def edit_task(self, index, new_title, new_description=""):
        """Edit a task by index"""
        if 0 <= index < len(self.tasks):
            self.tasks[index].edit(new_title, new_description)

    def mark_done(self, index):
        """Mark a task as done by index"""
        if 0 <= index < len(self.tasks):
            self.tasks[index].mark_done()

    def find_task_by_title(self, title):
        """Search task by title"""
        for task in self.tasks:
            if task.title == title:
                return task
        return None
    
    def show_tasks(self):
        """Display all tasks"""
        if not self.tasks:
            print("❌ No tasks registered.")
        else:
            for i, task in enumerate(self.tasks):
                print(f"{i}. {task}")


# ---------------- Sample Run ----------------
if __name__ == "__main__":
    manager = TaskManager()

    # Add some sample tasks
    manager.add_task("Study Python", "Finish OOP lesson")
    manager.add_task("Go Shopping", "Buy milk and bread")
    manager.add_task("Workout", "30 minutes running")

    # Display tasks
    print("\n📌 Task List:")
    manager.show_tasks()

    # Mark the second task as done
    manager.mark_done(1)

    # Edit the first task
    manager.edit_task(0, "Study Python", "Finish OOP + Exceptions")

    # Display after changes
    print("\n📌 Updated Task List:")
    manager.show_tasks()
