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