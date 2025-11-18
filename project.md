# Master Prompt for AI Coding Agent (Final Edition with Icon Customization)

**Objective:** Build **Project Gyron**, a complete GitHub Pages application that provides a frictionless, web-hosted utility for creating Progressive Web Apps (PWAs) from a single URL, with support for custom and pre-packaged icons.

**Primary Directive:** The entire project must be structured and coded for zero-configuration deployment to a personal GitHub Pages repository. You will generate a complete project folder, including the application file (`index.html`), a deploy-ready `README.md`, and all supporting documentation. You are to implement the UI to match the **text-based mockups** provided in the `design.md` document, including the full icon customization functionality.

---

### **Project Structure and Documentation Generation**

Generate a complete project folder structured for immediate use as a GitHub repository.

1.  **Root Directory Files:**
    *   `index.html`: The single-file web application. **It must be named `index.html`** to ensure it works with GitHub Pages out of the box.
    *   `README.md`: A deployment-centric README file. The content is specified below.
    *   `AGENTS.md`: The project memory document.

2.  **`docs/` Directory:**
    *   Create a folder named `docs`.
    *   Place the following specification documents inside: `requirements.md`, `design.md`, `tasks.md`.

Adhere strictly to the content defined in the following specification documents.

---

### **1. `docs/requirements.md` (Product Requirements Document)**

#### **1.1. Project Overview**

Project Gyron is a GitHub Pages application that enables users to create a functional desktop PWA from a URL. It solves the SSO/redirect issue by programmatically generating a PWA with a persistent `start_url` and allows for icon customization. The project is architected specifically for deployment on GitHub Pages to leverage its free, secure (HTTPS) hosting.

*   **Goal:** Provide a zero-friction, browser-based tool to create PWAs with custom icons that correctly handle complex authentication flows.
*   **Scope:** A single-page web application (`index.html`) with icon selection and its supporting documentation, optimized for GitHub Pages.

#### **1.2. User Stories & Acceptance Criteria**

*   **US-101: Core PWA Generation from GitHub Pages**
    *   **As a** user,
    *   **I want to** navigate to the Project Gyron GitHub Pages URL in my browser of choice,
    *   **so that** I can create a desktop app that leverages that specific browser's cookies and SSO sessions.
    *   **Acceptance Criteria:**
        *   When a user visits the hosted `index.html` URL, it presents an input field and a "Create App" button.
        *   After entering a target URL and clicking, the UI updates to show an "Install App" button.
        *   The PWA installs into the browser that is currently visiting the GitHub Pages site.

*   **US-102: App Icon Customization**
    *   **As a** user,
    *   **I want to** either upload my own icon or select from a list of generic icons before creating my app,
    *   **so that** my installed PWA has a distinct and relevant appearance on my desktop.
    *   **Acceptance Criteria:**
        *   The UI provides a clear choice between uploading a file or selecting from a pre-defined icon gallery.
        *   If a custom icon is uploaded, it is correctly displayed on the final installed PWA.
        *   If a generic icon is selected, it is correctly displayed on the final installed PWA.
        *   A default icon is used if no selection is made.

---

### **2. `docs/design.md` (Technical Architecture + User Flow/UI/UX Document)**

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

---

### **3. `docs/tasks.md` (BMAD-Method Inspired Task Breakdown)**

#### **Cycle 1: Core Logic & Local Simulation**

*   **BUILD:**
    *   `T-101`: Create `index.html` with the basic UI (URL input and Create button only).
    *   `T-102`: Write JS to dynamically generate and register a basic Service Worker and implement `postMessage` communication.
*   **MEASURE:**
    *   `M-101`: Simulate the GitHub Pages environment with a local server (`python -m http.server`). Verify worker registration and communication.
*   **ANALYZE:** The core logic is viable.
*   **DECIDE:** Proceed to dynamic manifest generation.

#### **Cycle 2: Dynamic Manifest & Installation**

*   **BUILD:**
    *   `T-201`: Enhance the worker to intercept `manifest.json` requests and respond with a synthetic manifest.
    *   `T-202`: Implement the UI update to show the "Install App" button using the `beforeinstallprompt` event.
*   **MEASURE:**
    *   `M-201`: Test via local server. Verify a basic PWA (without custom icon) can be installed.
*   **ANALYZE:** The end-to-end installation workflow is functional.
*   **DECIDE:** Proceed to add the icon customization feature.

#### **Cycle 3: Icon Customization**

*   **BUILD:**
    *   `T-301`: Add the icon selection UI to `index.html` as per the mockup.
    *   `T-302`: Pre-encode 5-6 icons as Base64 `dataURL`s and store them in a JS array.
    *   `T-303`: Implement the `FileReader` logic for the custom icon upload button.
    *   `T-304`: Update the main JS logic to pass the selected icon `dataURL` to the Service Worker.
    *   `T-305`: Update the Service Worker to receive and inject the icon `dataURL` into the `manifest.json`.
*   **MEASURE:**
    *   `M-301`: Test both generic icon selection and custom icon upload. Verify the chosen icon appears on the final installed PWA.
*   **ANALYZE:** The icon customization feature is fully functional and self-contained.
*   **DECIDE:** The application is feature-complete. Finalize documentation.

#### **Cycle 4: Documentation for Deployment**

*   **BUILD:**
    *   `T-401`: Create the deployment-centric `README.md`.
    *   `T-402`: Create `AGENTS.md` and all documents in the `docs/` folder.
*   **MEASURE:**
    *   `M-401`: Review all generated documents for clarity and accuracy.
*   **ANALYZE:** The project is fully documented and ready for deployment.
*   **DECIDE:** The project is complete.

---

### **4. `AGENTS.md` (Project Memory Document)**

*   **PROJECT_IDENTITY:**
    *   Name: Project Gyron
    *   Purpose: A GitHub Pages application for creating robust, customizable PWAs.
*   **TECHNICAL_DECISIONS:**
    *   **Decision 001: GitHub Pages as Primary Deployment Target.** Rationale: Mandatory for the `https://` context required by Service Workers.
    *   **Decision 002: Vanilla JavaScript.** Rationale: Avoids dependencies, maximizing simplicity.
    *   **Decision 003: Text-Based Mockup Driven UI.** Rationale: To ensure a predictable and non-ambiguous user interface.
    *   **Decision 004: Self-Contained Icon Handling.** Rationale: To provide icon customization without external dependencies, both user uploads and a generic icon set are handled by converting images to Base64 `dataURL`s. This keeps the application as a single, portable `index.html` file.
*   **RISK_ASSESSMENT:**
    *   **Risk 01 (Low): User Confusion.** A user might download `index.html` and try to open it locally. Mitigation: The `README.md` will prominently feature the live demo link.

---

### **Content for `README.md`**

**Directive:** The `README.md` file must be generated with the following content.

```markdown
# Project Gyron

**Live Demo:** [https://YOUR-USERNAME.github.io/project-gyron](https://YOUR-USERNAME.github.io/project-gyron) _(Replace this link after deployment)_

A simple, zero-dependency web tool for creating persistent Progressive Web Apps (PWAs) from any URL, with custom icons.

## Why This Exists

Many modern web services, especially internal corporate tools, use Single Sign-On (SSO) that redirects you through several URLs before landing on the final application. If you try to use your browser's built-in "Install App" or "Save as App" feature, it often saves the temporary, post-authentication URL. This means the next time you launch the "app," it fails because the authentication is missing.

Project Gyron solves this by allowing you to create a PWA that **always** starts from a specific URL you provide, ensuring the proper authentication flow runs every single time.

## How to Use

1.  Navigate to the **Live Demo** link above in the browser you want the app to be installed in (e.g., Edge for work apps, Chrome for personal apps).
2.  Paste the stable, initial URL for your web service into the input box.
3.  Optionally, select a generic icon or upload your own.
4.  Click "Create App."
5.  Click the "Install App" button that appears.
6.  The app will be installed on your desktop with your chosen icon, using the browser profile you started with.

## Deploy Your Own Version

This tool is designed to be easily forked and hosted on your own GitHub account.

1.  **Fork this Repository:** Click the "Fork" button at the top-right of this page.
2.  **Enable GitHub Pages:** In your forked repository, go to `Settings` > `Pages`. Under "Build and deployment," select `Deploy from a branch` as the source, and choose the `main` branch with the `/ (root)` folder. Save your changes.
3.  **Done!** Your personal version of Project Gyron will be live at `https://YOUR-USERNAME.github.io/YOUR-REPO-NAME` within a few minutes.
```
