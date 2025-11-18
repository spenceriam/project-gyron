# Project Gyron

**A simple, zero-dependency web tool for creating persistent Progressive Web Apps (PWAs) from any URL, with custom icons.**

## Why This Exists

Many modern web services, especially internal corporate tools, use Single Sign-On (SSO) that redirects you through several URLs before landing on the final application. If you try to use your browser's built-in "Install App" feature, it often saves the temporary, post-authentication URL. This means the next time you launch the "app," it fails because the authentication is missing.

Project Gyron solves this by allowing you to create a PWA that **always** starts from the specific URL you provide, ensuring the proper authentication flow runs every single time.

## How to Use

1.  Navigate to the **Live Demo** link for this repository's GitHub Pages site.
2.  Paste the stable, initial URL for your web service into the input box.
3.  Enter a custom name for your app.
4.  Optionally, select a generic icon or upload your own.
5.  Click "Create App."
6.  Click the "Install App" button that appears.
7.  The app will be installed on your desktop, using the browser profile you started with.

## Deploy Your Own Version

This tool is designed to be easily forked and hosted on your own GitHub account.

1.  **Fork this Repository:** Click the "Fork" button at the top-right of this page.
2.  **Enable GitHub Pages:** In your forked repository, go to `Settings` > `Pages`.
3.  Under "Build and deployment," select `Deploy from a branch` as the source.
4.  Choose the `main` branch with the `/ (root)` folder and click `Save`.
5.  **Done!** Your personal version of Project Gyron will be live at `https://YOUR-USERNAME.github.io/YOUR-REPO-NAME` within a few minutes.
