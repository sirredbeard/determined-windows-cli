# Determined AI Windows CLI 

This project is primarily at GitHub Actions workflow that:

- Checks for new releases of [Determined AI](https://github.com/determined-ai/determined) daily
- Compares it against the current release of Determined AI Windows CLI here
- If a newer release of Determined AI is detected, it will:
    - Check out the latest release of Determined AI
    - Build the Determined AI CLI client on Windows as a binary using [PyInstaller](https://pyinstaller.org/)
    - Release the Determined AI CLI build for Windows and binary as a release with a matching release version as a .zip file

## Installation

PRs for inclusion in [winget](https://github.com/microsoft/winget-pkgs/pull/133503) and [Scoop](https://github.com/ScoopInstaller/Extras/pull/12583) are pending.

In the interim, the following steps will download and install the latest version of the CLI to ~\Determined and add the folder to your path:

```powershell
$response = Invoke-RestMethod -Uri $latestReleaseUrl
$zipUrl = $response.assets | Where-Object { $_.name -like "*.zip" } | Select-Object -ExpandProperty browser_download_url
Invoke-WebRequest -Uri $zipUrl -OutFile determined-cli.zip
$destDir = Join-Path -Path $HOME -ChildPath "Determined"
New-Item -ItemType Directory -Path $destDir | Out-Null
Expand-Archive -Path $zipFile -DestinationPath $destDir -Force
$env:Path += ";$destDir"
[System.Environment]::SetEnvironmentVariable("Path", $env:Path, [System.EnvironmentVariableTarget]::User)
```

## Help

Join the [Determined AI Commmunity Slack](https://join.slack.com/t/determined-community/shared_invite/zt-1f4hj60z5-JMHb~wSr2xksLZVBN61g_Q).

## License

This project is licensed under the Apache License Version 2.0.