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