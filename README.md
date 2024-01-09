Determined AI Windows CLI 

This project is primarily at GitHub Actions workflow that:

- Checks for new releases of [Determined AI](https://github.com/determined-ai/determined) daily
- Compares it against the current release of Determined AI Windows CLI here
- If a newer release of Determined AI is detected, it will:
    - Check out the latest release of Determined AI
    - Build the Determined AI CLI client on Windows as a binary using [PyInstaller](https://pyinstaller.org/)
    - Release the Determined AI CLI build for Windows and binary as a release with a matching release version as a .zip file