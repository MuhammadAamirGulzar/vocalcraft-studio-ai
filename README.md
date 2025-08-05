# Vocal Craft: AI-Powered Content Creation

## Video Demo

https://github.com/user-attachments/assets/daf8e887-c946-4290-8b5c-69b0d29ad67b

## Results

![results (1)](https://github.com/user-attachments/assets/69e0efff-9e88-4eb0-b31a-a449c84f0f68)
![results (5)](https://github.com/user-attachments/assets/1f0c97f0-7fa5-4770-979a-c6fd834a863e)
![results (4)](https://github.com/user-attachments/assets/cd013e7a-7e4e-4097-9358-9af8e83a494d)
![results (3)](https://github.com/user-attachments/assets/6c5a49cf-eddf-4933-8b33-f59a91a04783)
![results (2)](https://github.com/user-attachments/assets/a937e219-e285-4262-ba84-aff167ea5c9d)

## Overview

Vocal Craft is an Android application that leverages AI to empower users in creating visual content, such as posters, social media graphics, and other visual materials. The application accepts voice and text prompts, allows users to upload their own images, and utilizes AI for generating and editing the content.

## Core Features

*   **Authentication:**
    *   Google Sign-In
    *   Email/Password Sign-In & Sign-Up
*   **Image Input:**
    *   Users can upload images accompanied by captions.
    *   Images are stored on Dropbox.
    *   Image metadata is stored on Firebase.
*   **Prompt-Based Generation:**
    *   Accepts direct text prompts.
    *   Accepts voice prompts, which are transcribed using an API, and the resulting text is used.
    *   Sends prompts to an API for Named Entity Recognition (NER) and to establish an initial content structure.
*   **Dynamic Content Editing (NER Form):**
    *   Displays NER results in an editable form.
    *   Allows users to modify the extracted information.
    *   Saves the refined content structure to Firebase.
*   **Visual Canvas (SVG/Image Editor):**
    *   Generates a visual composition based on the refined NER data and a matched uploaded image.
    *   Allows dragging, resizing, and rotating of text elements.
    *   Allows editing of text content, font, size, and color.
    *   Allows dragging and resizing of a primary object image.
    *   Supports object replacement via inpainting:
        *   The user provides a caption.
        *   The system finds a matching uploaded image.
        *   An API provides a masked version of the image to replace the object.
*   **Image Resizing & Output:**
    *   Resizes the final creation to various aspect ratios (e.g., Square, Portrait, Landscape) using an API.
    *   Saves the final image to the device gallery.
    *   Uploads the final image to Dropbox.
*   **Prompt History:**
    *   Saves past text prompts for easy reuse.
*   **User Profile (Partial Implementation):**
    *   UI for setting company name and theme colors.
    *   Saving functionality is not fully implemented.
*   **Templates (Read-Only):**
    *   Displays a sample template structure.

## Setup Instructions

### Prerequisites
*   Android Studio (latest stable version recommended)
*   Firebase Account ([https://firebase.google.com/](https://firebase.google.com/))
*   Dropbox Account ([https://www.dropbox.com/](https://www.dropbox.com/)) for image storage.
*   Access to the external APIs (currently hosted at `http://35.171.159.55:8000`). Ensure this endpoint is accessible.

### 1. Clone the Repository
```bash
git clone <repository_url>
cd <repository_directory>
```
(Replace `<repository_url>` and `<repository_directory>` with actual values if known, otherwise use placeholders.)

### 2. Firebase Setup
1.  Go to the [Firebase console](https://console.firebase.google.com/).
2.  Create a new project (or use an existing one).
3.  Add an Android app to your Firebase project:
    *   **Package name:** `com.aliashraf.vocalcraft` (You can find this in `app/build.gradle.kts` -> `namespace` or `applicationId`).
    *   Provide a nickname (optional).
    *   Download the `google-services.json` file.
4.  Place the downloaded `google-services.json` file into the `app/` directory of your cloned project.
5.  In the Firebase console, enable the following services:
    *   **Authentication:** Enable "Google" and "Email/Password" sign-in methods.
    *   **Realtime Database:** Create a database (choose appropriate rules for development, e.g., test mode, or secure rules for production).
    *   **Storage (Optional but Recommended):** While the app currently uses Dropbox for primary image uploads, Firebase Storage might be used or integrated later. It's good practice to enable it.

### 3. Dropbox Setup
1.  Go to the [Dropbox App Console](https://www.dropbox.com/developers/apps) and create a new app.
    *   Choose "Scoped access."
    *   Choose "Full Dropbox" or "App folder" access depending on your preference (App folder is generally safer).
    *   Give your app a unique name.
2.  Once the app is created, go to the "Permissions" tab and ensure the following are checked:
    *   `files.content.write`
    *   `files.content.read`
    *   `sharing.write` (to create shared links)
3.  Go to the "Settings" tab and find the "Generated access token". Generate one if it's not already there.
4.  **Important:** This access token needs to be placed into the application code where Dropbox API calls are made. Currently, it's hardcoded in:
    *   `app/src/main/java/com/aliashraf/vocalcraft/ImageInsertActivity.kt`
    *   `app/src/main/java/com/aliashraf/vocalcraft/SvgActivity.kt`
    *   Replace the placeholder `dropboxAccessToken = "YOUR_ACCESS_TOKEN"` with your actual generated token in these files.
    *   **Security Note:** For production apps, hardcoding access tokens is not recommended. Consider using a secure backend to manage tokens or using Android's Keystore system.

### 4. API Endpoint Configuration
The application relies on external APIs for transcription, NER, image generation, inpainting, and resizing. These are currently hardcoded to `http://35.171.159.55:8000`.
*   Ensure this endpoint is correct and accessible from your development environment/device.
*   If the API endpoint changes, you will need to update it in the following files:
    *   `app/src/main/java/com/aliashraf/vocalcraft/PromptActivity.kt` (for `/transcribe` and `/ner`)
    *   `app/src/main/java/com/aliashraf/vocalcraft/SvgActivity.kt` (for `/generate_image`, `/inpainting`, and `/resizer`)

### 5. Build and Run
1.  Open the cloned project in Android Studio.
2.  Let Android Studio sync Gradle files and download dependencies. This might take a few minutes.
3.  If prompted, ensure you have the correct Android SDK versions installed (target SDK is 34, min SDK is 24, compile SDK is 34, as per `app/build.gradle.kts`).
4.  Connect an Android device or start an emulator.
5.  Click the "Run" button (green play icon) in Android Studio.

---

## Additional Notebooks

### `sdxl-training-actual.ipynb`
This notebook outlines the process of fine-tuning a Stable Diffusion XL (SDXL) model using LoRA (Low-Rank Adaptation) with DreamBooth. Key aspects:

- **Setup**:
  - Uses Hugging Face's `diffusers`, `transformers`, and other utilities.
  - Environment is initialized with authentication to Hugging Face Hub.
  
- **Configuration**:
  - Custom configuration for model paths, instance prompts, learning rates, and output directories.
  - Includes options for resolution, precision (fp16), number of training steps, and checkpointing.

- **Training**:
  - Launches the training script `train_dreambooth_lora_sdxl.py` using a subprocess call with appropriate arguments.
  - Uses LoRA modules to speed up and reduce memory requirements for fine-tuning.

- **Output**:
  - The fine-tuned model is saved in the specified output directory.
  - Trained weights can be pushed to Hugging Face Hub for sharing.

### `apicaller.ipynb`
This notebook demonstrates how to interact with the fine-tuned model hosted on Hugging Face Hub:

- **Model Inference via API**:
  - Uses `requests` to call the inference API for the SDXL model.
  - Takes a text prompt and returns a generated image in base64 format.
  - Decodes the base64 image and displays it using PIL.

- **Authorization**:
  - Requires Hugging Face API token for authenticated access.

- **Utility**:
  - Useful for testing and showcasing model capabilities directly from a notebook.
  - Can be extended to integrate with front-end applications or mobile apps.


### Additional Notes
*   **Dependencies:** The project uses several third-party libraries (e.g., Firebase, OkHttp, Glide, Picasso, AmbilWarnaDialog). These are managed by Gradle and listed in `app/build.gradle.kts` and `gradle/libs.versions.toml`.
*   **Permissions:** The app requests permissions like `RECORD_AUDIO`, `INTERNET`, and storage permissions. Ensure these are granted on the device when prompted.
*   **API Keys Security:** The current setup includes hardcoded API keys (Dropbox token) and IP addresses. For a production environment, these should be secured appropriately (e.g., using environment variables, a secure backend proxy, or Android Keystore). 


