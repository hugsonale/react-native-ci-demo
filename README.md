

This repository demonstrates a simple Continuous Integration (CI) pipeline for a React Native Android application using GitHub Actions.

The main paurpose of this project is to show how an Android build can be automated, how environment variables can be managed securely, and how the generated build could be distributed in a real-world scenario.

**How the CI Pipeline Works**

The CI pipeline is implemented using GitHub Actions and is defined in the file: .github/workflows/ci.yml

# The pipeline is triggered automatically when:

- Code is pushed to the main branch
- A pull request is opened against the main branch

During execution, the pipeline performs the following actions:

- Takes a look at the repository's source code
- Gets Node.js ready to use.
- Uses npm to install project requirements.
- JDK 17 is set up for Android builds.
- Sets up the Android SDK
- Use Gradle to build the Android app.
- Uploads the APK that was made as a build artifact

If all steps complete successfully, the workflow finishes with a usable Android APK.


# Environment Variable Management

Environment variables are managed securely using GitHub Actions Secrets.

Instead of hardcoding configuration values in the source code, they are stored in the repository settings under GitHub Secrets. Like:
- API_URL
- APP_ENV

During the CI run, these secrets are injected at runtime and written into a temporary .env file. This file exists only during the workflow execution and is never committed to the repository. This Prevents sensitive configuration from being exposed, allows easy changes without modifying source code and supports multiple environments such as development and production.

# Build Automation Steps

- The automated build process follows these steps:
- Install Node.js dependencies using npm install
- Prepare the Android build environment (Java and Android SDK)
- Grant execution permission to the Gradle wrapper
- Run the Gradle command to generate a debug APK
- Store the APK as a GitHub actions artifact

This confirms that the CI pipeline is able to produce a valid Android build automatically.

# Theoretical cloud deployment process

This project focuses on CI only. No actual deployment is performed.

However, in a real production setup, the generated Android build could be distributed using one of the following approaches:

# Firebase App Distribution

The CI pipeline could authenticate using a Firebase service account and upload the APK or AAB to Firebase App Distribution. This allows internal testers to receive and test the app before release.

# Google Play Console Internal Testing

Alternatively, the build could be uploaded to the Google Play Console using the Internal Testing track. This enables controlled testing with selected users and provides access to Play Store signing, analytics, and crash reporting.

These deployment steps are intentionally kept theoretical, as required by the task.