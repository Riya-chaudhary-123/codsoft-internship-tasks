import os
import json

# File to store the tasks
FILE_NAME = "todo_list.json"

# Load tasks from file
def load_tasks():
    if os.path.exists(FILE_NAME):
        with open(FILE_NAME, "r") as file:
            return json.load(file)
    return []

# Save tasks to file
def save_tasks(tasks):
    with open(FILE_NAME, "w") as file:
        json.dump(tasks, file, indent=4)

# Display tasks
def show_tasks(tasks):
    if not tasks:
        print("\n📭 No tasks available.")
    else:
        print("\n📋 Your To-Do List:")
        for i, task in enumerate(tasks, 1):
            status = "✅" if task["done"] else "❌"
            print(f"{i}. {task['task']} [{status}]")

# Add a new task
def add_task(tasks):
    task_name = input("Enter the new task: ")
    tasks.append({"task": task_name, "done": False})
    print("✅ Task added!")

# Mark task as done
def mark_done(tasks):
    show_tasks(tasks)
    try:
        task_num = int(input("Enter task number to mark as done: "))
        if 0 < task_num <= len(tasks):
            tasks[task_num - 1]["done"] = True
            print("✅ Task marked as done.")
        else:
            print("⚠️ Invalid task number.")
    except ValueError:
        print("⚠️ Please enter a valid number.")

# Delete a task
def delete_task(tasks):
    show_tasks(tasks)
    try:
        task_num = int(input("Enter task number to delete: "))
        if 0 < task_num <= len(tasks):
            removed = tasks.pop(task_num - 1)
            print(f"🗑️ Task '{removed['task']}' deleted.")
        else:
            print("⚠️ Invalid task number.")
    except ValueError:
        print("⚠️ Please enter a valid number.")

# Main menu loop
def main():
    tasks = load_tasks()
    while True:
        print("\n----- TO-DO LIST MENU -----")
        print("1. Show Tasks")
        print("2. Add Task")
        print("3. Mark Task as Done")
        print("4. Delete Task")
        print("5. Exit")

        choice = input("Choose an option (1-5): ")

        if choice == "1":
            show_tasks(tasks)
        elif choice == "2":
            add_task(tasks)
        elif choice == "3":
            mark_done(tasks)
        elif choice == "4":
            delete_task(tasks)
        elif choice == "5":
            save_tasks(tasks)
            print("👋 Goodbye! Your tasks are saved.")
            break
        else:
            print("⚠️ Invalid choice. Try again.")

if __name__ == "__main__":
    main()
