# Task Tracker CLI (Java)

Welcome to the Task Tracker CLI, a simple, lightweight, and dependency-free command-line application for managing your daily tasks. Written in pure, vanilla Java, this tool allows you to add, update, delete, and list your tasks directly from the terminal.

All tasks are persistently stored in a `tasks.json` file in the project's root directory, ensuring your data is always available.

## Features

* **Add Task:** Create a new task with a description.
* **Update Task:** Modify the description of an existing task.
* **Delete Task:** Remove a task from your list by its ID.
* **Change Status:** Mark tasks as "in progress" or "done".
* **List Tasks:** View all tasks or filter them by status (`todo`, `in-progress`, `done`).
* **Persistent Storage:** All tasks are saved to `tasks.json` after every operation, so you never lose your data.

---

## Technology Stack

This project is intentionally built with **zero external dependencies** to keep it simple and demonstrate core Java principles. No Maven, no Gradle, no JSON libraries.

* **Java (JDK 11+):**
    * Written entirely in pure Java.
    * Uses modern Java features like `java.nio.file.Path` and `java.nio.file.Files` (from Java 11) for efficient file reading and writing.
    * Uses `java.time.LocalDateTime` and `java.time.format.DateTimeFormatter` for accurate timestamping (`createdAt`, `updatedAt`).
    * Uses `Enum` for strongly-typed task statuses (`TODO`, `IN_PROGRESS`, `DONE`).
    * Uses the **Stream API** (`.stream().filter()...`) for efficient in-memory searching of tasks.

* **Custom JSON Parser:**
    * To adhere to the "no external libraries" rule, the project does not use Jackson or Gson.
    * Instead, it features a simple, hand-written JSON parser in the `Task.java` class.
    * `Task.toJson()`: Manually builds a JSON string from a Task object.
    * `Task.fromJson(String json)`: Manually parses a JSON string into a new Task object using basic string manipulation (`.split()`, `.replace()`, `.strip()`).

---

## Getting Started

### Prerequisites

You only need one thing installed on your system:
* **Java Development Kit (JDK) 11** or newer. (Java 11 is required for `Files.readString` and `String.isBlank` methods used in the code).

### Installation & Running

1.  **Download the Code:**
    * **Option 1 (Git):** Clone this repository:
        ```bash
        git clone [https://github.com/P3ngu1n-23/Task_CLI.git](https://github.com/P3ngu1n-23/Task_CLI.git)
        cd Task_CLI
        ```
    * **Option 2 (ZIP):** Download the ZIP file from GitHub and extract it.

2.  **Compile the Code:**
    * Open your terminal (Command Prompt, PowerShell, etc.) and navigate into the project directory (where the `.java` files are located).
    * Run the Java compiler (`javac`) to compile all the source files at once:

    ```bash
    javac TaskApp.java TaskManager.java Task.java Status.java
    ```
    * This will create the necessary `.class` files in the same directory.

3.  **Run the Application:**
    * You can now run the application using the `java` command, followed by the main class (`TaskApp`) and your desired command.

    ```bash
    java TaskApp <command> [arguments]
    ```
    * See the **Usage** section below for all available commands.

---

## Usage (Available Commands)

The application is run by passing commands and arguments directly into the terminal.

### Add a new task
Adds a new task with a "Todo" status.
* **Command:** `add`
* **Usage:**
    ```bash
    java TaskApp add "<your_task_description>"
    ```
* **Example:**
    ```bash
    java TaskApp add "Buy groceries and cook dinner"
    ```
    *(Note: Use quotes "" if your description contains spaces.)*

### List tasks
Lists tasks. Defaults to "All" if no status is provided.
* **Command:** `list`
* **Usage:**
    ```bash
    java TaskApp list
    java TaskApp list todo
    java TaskApp list in-progress
    java TaskApp list done
    ```
* **Example (List all):**
    ```bash
    java TaskApp list
    ```
* **Example (List only done):**
    ```bash
    java TaskApp list done
    ```

### Update a task
Updates the description of an existing task by its ID.
* **Command:** `update`
* **Usage:**
    ```bash
    java TaskApp update <ID> "<new_description>"
    ```
* **Example:**
    ```bash
    java TaskApp update 1 "Buy groceries and cook dinner"
    ```

### Mark as "In Progress"
Changes a task's status to "In progress".
* **Command:** `mark-in-progress`
* **Usage:**
    ```bash
    java TaskApp mark-in-progress <ID>
    ```
* **Example:**
    ```bash
    java TaskApp mark-in-progress 1
    ```

### Mark as "Done"
Changes a task's status to "Done".
* **Command:** `mark-done`
* **Usage:**
    ```bash
    java TaskApp mark-done <ID>
    ```
* **Example:**
    ```bash
    java TaskApp mark-done 1
    ```

### Delete a task
Permanently removes a task by its ID.
* **Command:** `delete`
* **Usage:**
    ```bash
    java TaskApp delete <ID>
    ```
* **Example:**
    ```bash
    java TaskApp delete 1
    ```

### Show Help (Default)
If you run the application with no commands, it will display the usage guide.
* **Example:**
    ```bash
    java TaskApp
    ```
