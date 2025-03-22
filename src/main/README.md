# Core Electron Application

## 1. Main.ts `main.ts`
The `main.ts` file in this repository is used to set up and manage the main process of an Electron application. Here are its key functions:

- **Electron Main Process**: This module runs inside Electron's main process and is responsible for starting the renderer process and handling communication between processes using IPC (Inter-Process Communication).
- **Application Updater**: Implements an updater (`AppUpdater`) that uses `electron-updater` to check for updates and notify the user.
- **Window Management**: Creates and manages the main application window, including configuring its properties (size, icon, preload script), loading the initial HTML file, and handling window events.
- **Development Tools**: Installs development extensions like React Developer Tools when in development mode.
- **Menu Building**: Constructs and sets the application menu using the `MenuBuilder` class.
- **Auto Updates**: Initiates the auto-update process if the app uses auto-updates.
- **Event Listeners**: Adds event listeners to handle application lifecycle events such as window closing and application activation.

This file is compiled to `./src/main.js` using Webpack, optimizing performance for the production build.

---

## 2. Menu.ts `menu.ts`
The `menu.ts` file in your repository is used to create and manage the application menu for an Electron application. Here's a breakdown of its key functionalities:

1. **MenuBuilder Class**: This class is responsible for building and setting the application menu.
    - **Constructor**: Takes an instance of `BrowserWindow` and assigns it to `this.mainWindow`.
    - **buildMenu()**: Builds the menu based on the operating system (macOS or others) and environment (development or production). It calls `setupDevelopmentEnvironment()` if in development mode and sets up the appropriate menu template.
    - **setupDevelopmentEnvironment()**: Adds a context menu with an "Inspect element" option in development mode.
    - **buildDarwinTemplate()**: Constructs the menu template for macOS, including standard menus like "File", "Edit", "View", "Window", and "Help".
    - **buildDefaultTemplate()**: Constructs the default menu template for other operating systems, including menus like "File", "View", and "Help".

2. **Menu Items**: The file defines various menu items and their actions, such as:
    - **Reload**: Reloads the window's contents.
    - **Toggle Full Screen**: Toggles the window between full-screen mode and normal mode.
    - **Toggle Developer Tools**: Opens or closes the developer tools.
    - **Open**: Placeholder for opening files.
    - **Close**: Closes the main window.
    - **About**: Provides information about the application.
    - **Help**: Provides links to external resources like documentation, community discussions, and issue tracking.

Overall, this file is essential for setting up the user interface menus in an Electron application, providing both basic navigation and developer tools access.

---

## 3. Preload.ts `preload.ts`
The `preload.ts` file is used in Electron applications to expose a limited API to the renderer process while keeping the main process secure. Here's a breakdown of what it does:

1. **Imports**:
   - `contextBridge`, `ipcRenderer`, and `IpcRendererEvent` are imported from the `electron` module.

2. **Type Definitions**:
   - Defines a type `Channels` which currently includes the string `'ipc-example'`.

3. **Electron Handler**:
   - Creates an `electronHandler` object that includes methods to handle IPC (Inter-Process Communication):
     - `sendMessage`: Sends messages to a specific channel.
     - `on`: Listens for messages on a specific channel and executes a provided callback function.
     - `once`: Listens for a single message on a specific channel and executes a provided callback function.

4. **Context Bridge**:
   - Uses `contextBridge.exposeInMainWorld` to expose the `electronHandler` object to the renderer process under the global variable `electron`.

This setup allows the renderer process to communicate with the main process securely using the defined API, preventing direct access to Node.js and Electron internals.

---

## 4. Util.ts `util.ts`
The `util.ts` file in your repository contains utility functions. Specifically, it includes a function `resolveHtmlPath` that resolves the path to an HTML file based on the environment.

Here's a detailed explanation of the function:

- **resolveHtmlPath(htmlFileName: string)**
  - This function takes an HTML file name as an argument.
  - It checks if the environment is in development mode:
    - If it is, it constructs a URL pointing to `localhost` with a specified port (default is 1212) and appends the HTML file name to the URL path.
    - If it is not in development mode, it constructs a file URL pointing to the resolved path of the HTML file within the renderer directory.

This function is useful for determining the correct path to HTML files depending on whether the application is running in development or production mode.