# AGENTS.md for Project Gyron

## Project Overview
- **Name:** Project Gyron
- **Purpose:** A GitHub Pages application for creating robust, customizable Progressive Web Apps (PWAs) from a single URL. This tool is designed for zero-configuration deployment to a personal GitHub Pages repository.

## Technical Stack
- **Frontend:** Vanilla HTML5, CSS3, JavaScript (ES6+)
- **Deployment:** GitHub Pages
- **Key APIs:** Service Worker, `beforeinstallprompt`, `FileReader`, `postMessage`

## Development & Testing
- **Setup:** No dependencies are required. The project is a single `index.html` file.
- **Testing Environment:** To simulate the required HTTPS environment of GitHub Pages, run a local server. A simple way is to use Python's built-in server:
  ```bash
  python -m http.server
  ```
- **Verification:** After running the local server, navigate to `http://localhost:8000` in a PWA-compatible browser (e.g., Chrome, Edge) to test the full application workflow. The key success criteria are the ability to generate and install a PWA with a custom or generic icon.

## Project Directives & Decisions
- **Decision 001: GitHub Pages as Primary Deployment Target.**
  - **Rationale:** Mandatory for the `https://` context required by Service Workers.
- **Decision 002: Vanilla JavaScript.**
  - **Rationale:** Avoids dependencies, maximizing simplicity and portability. The entire application is self-contained in `index.html`.
- **Decision 003: Text-Based Mockup Driven UI.**
  - **Rationale:** To ensure a predictable and non-ambiguous user interface, as defined in `docs/design.md`.
- **Decision 004: Self-Contained Icon Handling.**
  - **Rationale:** To provide icon customization without external dependencies, both user uploads and a generic icon set are handled by converting images to Base64 `dataURL`s. This keeps the application as a single, portable `index.html` file.

## Risk Assessment
- **Risk 01 (Low): User Confusion.** A user might download `index.html` and try to open it locally via `file://`. This will not work due to browser security restrictions on Service Workers.
  - **Mitigation:** The `README.md` will prominently feature the live demo link and clear deployment instructions to guide users toward the correct (HTTPs) environment.
