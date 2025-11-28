print("1. Log in")
print("2. Exit")
first_choice = input("Enter your choice: ")
if first_choice == "2":
    print("Exiting Program...Goodbye!")
    exit()
elif first_choice != "1":
    print("Invalid choice. Exiting Program...")
    exit()

username = input("Enter your username: ")
password = input("Enter your password: ")
print("\nLog in successful! Welcome,", username)
print("-"*40)

tasks = []
running = True

while running:
    print(f"\n====WELCOME, {username.upper()}=====")
    print("1.Add Task")
    print("2.View Task")
    print("3.Edit Task")
    print("4.Mark Task Done")
    print("5.Logout")

    choice = input("Enter your choice: ")

    if choice == "1":
        adding = True
        while adding:
            title = input("\nTask Title: ")
            description = input("Task Description: ")
            due_date = input("Due Date: ")
            date_created = input("Date Created: ")

            task = {
                "Task Number": len(tasks) + 1,
                "Title": title,
                "Description": description,
                "Date Created": date_created,
                "Due Date": due_date,
                "Status": "Not Done"
            }

            tasks.append(task)
            print("\nTask added successfully!")

            add_more = input("Do you want to add another task? (yes/no): ").lower()
            if add_more != "yes":
                adding = False

    elif choice == "2":
        if tasks:
            print(f"\n=====LIST OF TASKS=====")
            for task in tasks:
                print(f"\nTask #{task['Task Number']}")
                print(f"Title: {task['Title']}")
                print(f"Description: {task['Description']}")
                print(f"Date Created: {task['Date Created']}")
                print(f"Due Date: {task['Due Date']}")
                print(f"Status: {task['Status']}")
                print("-" * 30)
        else:
            print("No tasks available")

    elif choice == "3":
        if tasks:
            print("\nWhich task do you want to edit?")
            for task in tasks:
                print(f"{task['Task Number']}. {task['Title']}")
            try:
                edit_num = int(input("Enter task number: "))
                if 1 <= edit_num <= len(tasks):
                    new_title = input("New Title: ")
                    new_desc = input("New Description: ")
                    new_due = input("New Due Date: ")

                    if new_title: tasks[edit_num - 1]["Title"] = new_title
                    if new_desc: tasks[edit_num - 1]["Description"] = new_desc
                    if new_due: tasks[edit_num - 1]["Due Date"] = new_due

                    print("Task updated successfully!")
                else:
                    print("Invalid task number.")
            except:
                print("Invalid input.")
        else:
            print("No tasks to edit.")

    elif choice == "4":
        if tasks:
            print("\nWhich task do you want to mark as done?")
            for task in tasks:
                print(f"{task['Task Number']}. {task['Title']}")
            try:
                done_num = int(input("Enter task number: "))
                if 1 <= done_num <= len(tasks):
                    tasks.pop(done_num - 1)
                    for i, t in enumerate(tasks):
                        t["Task Number"] = i + 1
                    print("Task marked as done and deleted!")
                else:
                    print("Invalid task number.")
            except:
                print("Invalid input.")
        else:
            print("No tasks to mark.")

    elif choice == "5":
        print("Logging out... Goodbye!")
        running = False

    else:
        print("Invalid choice. Try again.")

