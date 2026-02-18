### Set up the virtual environment

#### Option A: Windows (Recommended for PyCharm Community)
Since PyCharm Community Edition does not support WSL interpreters directly, run the environment natively on Windows.

1.  **Prerequisites:**
    - Install [Python 3.10+](https://www.python.org/downloads/) (Ensure "Add to PATH" is checked).
    - Install [Git for Windows](https://git-scm.com/download/win).

2.  **Run the Setup Script:**
    - Double-click `setup_windows.bat` in the project folder.
    - Or run in terminal:
      ```cmd
      setup_windows.bat
      ```

3.  **Configure PyCharm:**
    - Go to **File > Settings > Project > Python Interpreter**.
    - Click the gear icon > **Add...**
    - Select **Existing environment**.
    - Browse to: `C:\Users\msjen\PycharmProjects\google-deepmind-colabs\.venv\Scripts\python.exe`

#### Option B: WSL / Linux (Advanced)
If you prefer running in the terminal only or use VS Code.

1.  **Run the setup script:**
    ```bash
    chmod +x setup_wsl.sh
    ./setup_wsl.sh
    ```
