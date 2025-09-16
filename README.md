# Personal-task-tracker
A simple CRUD app for tracking daily tasks.
# Clone your repo to your machine
git clone https://github.com/<your-username>/task-tracker.git
cd task-tracker
task-tracker/
  ├─ src/        # code files
  ├─ tests/      # optional tests
  ├─ README.md
  └─ .gitignore
import json, os

FILE = "tasks.json"

def load_tasks():
    return json.load(open(FILE)) if os.path.exists(FILE) else []

def save_tasks(tasks):
    json.dump(tasks, open(FILE,"w"), indent=2)

def add_task(text):
    tasks = load_tasks()
    tasks.append({"task": text, "done": False})
    save_tasks(tasks)
    print(f"Added: {text}")

def list_tasks():
    for i,t in enumerate(load_tasks(),1):
        status = "✅" if t["done"] else "❌"
        print(f"{i}. {t['task']} {status}")

# basic CLI
if __name__ == "__main__":
    import sys
    if len(sys.argv) < 2:
        print("Usage: python app.py [add/list/done]")
    elif sys.argv[1] == "add":
        add_task(" ".join(sys.argv[2:]))
    elif sys.argv[1] == "list":
        list_tasks()
