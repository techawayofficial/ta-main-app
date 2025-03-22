# Core Electron Application

## Main.ts `main.ts`
The `main.ts` file in this repository is used to set up and manage the main process of an Electron application. Here are its key functions:

- **Electron Main Process**: This module runs inside Electron's main process and is responsible for starting the renderer process and handling communication between processes using IPC (Inter-Process Communication).
- **Application Updater**: Implements an updater (`AppUpdater`) that uses `electron-updater` to check for updates and notify the user.
- **Window Management**: Creates and manages the main application window, including configuring its properties (size, icon, preload script), loading the initial HTML file, and handling window events.
- **Development Tools**: Installs development extensions like React Developer Tools when in development mode.
- **Menu Building**: Constructs and sets the application menu using the `MenuBuilder` class.
- **Auto Updates**: Initiates the auto-update process if the app uses auto-updates.
- **Event Listeners**: Adds event listeners to handle application lifecycle events such as window closing and application activation.

This file is compiled to `./src/main.js` using Webpack, optimizing performance for the production build.