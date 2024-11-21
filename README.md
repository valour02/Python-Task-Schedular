# **Code Documentation**

## **Overview**
This script automates the scheduled execution of a Jupyter Notebook using Python. The notebook is converted to a Python script (or executed directly depending on the method), and the resulting Python script is executed at a specified time each day.

---

## **Modules Used**
1. **`schedule`**: A lightweight scheduling library that allows tasks to be run at specific times.
2. **`time`**: Used to introduce delays while the program checks for pending scheduled tasks.
3. **`subprocess`**: Executes shell commands from Python, allowing the script to convert and execute Jupyter Notebooks.

---

## **Code Explanation**

### **Function: `run_notebook(notebook_path)`**
This function handles the execution of a Jupyter Notebook.

#### **Parameters**:
- `notebook_path` (str): The file path of the Jupyter Notebook to be executed.

#### **Steps**:
1. **Convert Notebook to Python Script**:
   - The `subprocess.run()` method executes the command:
     ```
     jupyter nbconvert --to script <notebook_path>
     ```
   - Converts the specified `.ipynb` file into a `.py` script.
2. **Execute the Python Script**:
   - After conversion, the generated Python script is executed using:
     ```
     python <python_script_path>
     ```
3. **Error Handling**:
   - If the conversion or execution fails, an error message is displayed using the `except` block.
   - `subprocess.CalledProcessError` catches errors raised during the execution of the shell commands.

---

### **Global Variables**
- **`notebook_path`**:
  - Stores the file path of the Jupyter Notebook to be executed.
  - Example value: `r'Desktop/DATA ANALYTICS/General Codes/File Backup.ipynb'`.

---

### **Scheduling**
1. **Scheduling a Task**:
   - `schedule.every().day.at("11:19").do(run_notebook, notebook_path)`
   - Schedules the execution of the `run_notebook` function with the specified `notebook_path` every day at `11:19 AM`.

2. **Scheduler Execution**:
   - The program enters an infinite loop to continuously check for and run scheduled tasks:
     ```python
     while True:
         schedule.run_pending()
         time.sleep(1)
     ```

---

## **Second Method (Alternative Logic)**

The second part of the script uses a slightly different approach:
1. Executes the Jupyter Notebook directly using:
   ```
   jupyter nbconvert --to notebook --execute <notebook_path> --output <notebook_path>
   ```
   - Executes the notebook and saves the output back to the same file.
   - Includes a `--debug` option for troubleshooting.

---

## **Program Output**
- Displays a message indicating the scheduler is active:
  ```
  Scheduler is running...
  ```
- Executes the notebook at the scheduled time.
- If execution succeeds:
  ```
  Executed notebook: <notebook_path>
  ```
- If execution fails:
  ```
  Error executing notebook: <error details>
  ```

---

## **Applications**
- Automating data analysis workflows.
- Scheduling periodic updates for data-driven reports.
- Running computationally heavy notebooks at off-peak hours.

--- 

## **Limitations**
- Requires the `jupyter` executable to be available in the system's PATH.
- Does not handle non-deterministic outputs or interactive widgets in Jupyter Notebooks.

