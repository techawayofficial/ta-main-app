# ⚙️ Core Electron Application

## 🧠 Main.ts (main.ts)

The main.ts file sets up and manages the main process of the Electron application. Key functionalities include:

🖥 Electron Main Process: Runs inside Electron's main process, starts the renderer process, and handles IPC.

⬆️ Application Updater: Uses electron-updater to check for and notify users of updates.

🪟 Window Management: Manages the app window — size, icon, preload script — and loads the initial HTML file.

🛠 Development Tools: Installs tools like React Developer Tools when in development mode.

🍴 Menu Building: Constructs and sets the app menu via the MenuBuilder class.

🔁 Auto Updates: Initiates the auto-update process (when supported).

🎯 Event Listeners: Listens for lifecycle events like window closing and app activation.


> Compiled to: ./src/main.js via Webpack for optimized production builds.




---

## 🧾 Menu.ts (menu.ts)

The menu.ts file builds and manages the application menu. Key functionalities include:

🧱 MenuBuilder Class: Responsible for building and setting the app menu.

🛠 Constructor: Accepts a BrowserWindow and assigns it.

📜 buildMenu(): Builds menu templates based on OS (macOS vs others) and mode (dev vs prod).

🧪 setupDevelopmentEnvironment(): Adds dev tools like "Inspect Element" to the right-click menu.

🍏 buildDarwinTemplate(): Constructs macOS-specific menu layout.

💻 buildDefaultTemplate(): Creates menu for other platforms.


📋 Menu Items include:

🔄 Reload: Refreshes the app window.

🖥 Toggle Full Screen: Switch between full screen and windowed mode.

🔧 Toggle Developer Tools: Show/hide dev tools.

📂 Open: Placeholder to open files.

❌ Close: Closes the main app window.

ℹ️ About: Displays info about the app.

❓ Help: Links to docs, issues, and external resources.



This file is crucial for crafting the user’s navigation experience.


---

## 🧩 Preload.ts (preload.ts)

The preload.ts file exposes secure APIs to the renderer process. Key features include:

📦 Imports: Loads contextBridge, ipcRenderer, and IpcRendererEvent from Electron.

✍️ Type Definitions: Defines a Channels type (e.g., 'ipc-example').

⚡ Electron Handler: An electronHandler object that enables safe IPC:

sendMessage: Send message to a channel.

on: Listen for messages with a callback.

once: Listen once and auto-unsubscribe.


🔐 Context Bridge: Exposes electronHandler via contextBridge.exposeInMainWorld under the global electron.


> This ensures secure and controlled communication between main and renderer.




---

## 🛠 Util.ts (util.ts)

The util.ts file provides utility functions, specifically:

🧭 resolveHtmlPath(htmlFileName: string): Resolves the path to HTML files depending on the environment.

🔧 In dev mode:

Builds a localhost URL (default port 1212) with the specified file.


📦 In production:

Constructs a file:// URL to the bundled HTML file in the renderer directory.




> Ensures your app loads the correct HTML whether in development or production mode.
