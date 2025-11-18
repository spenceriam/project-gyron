#### **2.1. Technical Architecture**

*   **Technology Stack:** Vanilla HTML5, CSS3, JavaScript (ES6+).
*   **Deployment Target: GitHub Pages.** HTTPS hosting is mandatory for Service Worker functionality.
*   **System Architecture:** A dynamically registered Service Worker will serve a synthetic `manifest.json` from memory. This manifest will include a `dataURL` for the selected icon.

#### **2.2. User Flow**

1.  **Visit:** User opens the hosted Project Gyron URL.
2.  **Input:** User pastes their target URL.
3.  **Customize (Optional):** User selects a generic icon or uploads their own.
4.  **Create:** User clicks "Create App." The UI transitions to a "working" state.
5.  **Install:** The UI updates to a "ready" state, presenting an "Install App" button. User clicks it, and the native browser install prompt appears.

#### **2.3. Text-Based Mockups & UI Implementation Guide**

**Directive:** The UI **must** be implemented to closely match the following text-based mockups.

**State 1: Initial View**

```
+------------------------------------------------------+
|                                                      |
|                  Project Gyron                       |
|       Create a persistent web app from any URL       |
|                                                      |
|   +------------------------------------------------+ |
|   | Enter URL: https://...                         | |
|   +------------------------------------------------+ |
|                                                      |
|   Select an Icon:                                    |
|   +----+  +----+  +----+  +----+  +----+  +--------+ |
|   | 🌐 |  | ⚙️ |  | ☁️ |  | 💼 |  | ⭐ |  | Custom | |
|   +----+  +----+  +----+  +----+  +----+  +--------+ |
|                                                      |
|               +------------------+                   |
|               |    Create App    |                   |
|               +------------------+                   |
|                                                      |
+------------------------------------------------------+
```

**State 2: Ready to Install View**

```
+------------------------------------------------------+
|                                                      |
|               ✅ App Ready to Install!               |
|                                                      |
|   Your app will be installed using this browser's    |
|       profile (Edge, Chrome, etc.), preserving       |
|                 your logins and cookies.             |
|                                                      |
|            +--------------------------+              |
|            |  Install "Example App"   |              |
|            +--------------------------+              |
|                                                      |
+------------------------------------------------------+
```

**Implementation Notes for the Coding Agent:**

*   **Main Container:** Center a `max-width` container with a border, rounded corners, and a box shadow to create a "card" effect.
*   **Icon Handling (Critical):**
    *   **Generic Icons:** Pre-encode 5-6 professional, open-source icons (e.g., from Google Material Symbols) as Base64 `dataURL` strings and store them in a JavaScript array. The UI should render these as clickable buttons.
    *   **Custom Icon Upload:** The "Custom" button should trigger a hidden `<input type="file" accept="image/png, image/jpeg">`. When a user selects a file, use the `FileReader` API to read the file `asDataURL()`. This Base64 `dataURL` string becomes the icon.
    *   **Data Flow:** The selected `dataURL` (whether generic or custom) must be passed to the Service Worker alongside the target URL. The Service Worker will then inject this `dataURL` into the `icons` array of the `manifest.json` it generates.
*   **State Transition:** Toggle a CSS class on a main container to switch between the "Initial View" and the "Ready to Install View".