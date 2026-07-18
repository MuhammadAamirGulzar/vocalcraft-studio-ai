# VocalCraft Studio

AI-assisted creative production for ad-ready visuals from voice or text prompts.

## Product Summary

VocalCraft Studio is an Android application that turns user intent into editable marketing visuals. It combines prompt understanding, entity extraction, image composition, and responsive export workflows in a single production pipeline.

The system is designed for fast campaign iteration where users can:

- Input intent via text or voice
- Refine AI-structured content before generation
- Edit design output on a visual canvas
- Export final creatives in multiple aspect ratios

## Portfolio Value

This project demonstrates end-to-end AI product delivery:

- Mobile client architecture for AI-first UX
- Real-time backend integrations (transcription, NER, generation, inpainting, resizing)
- Cloud data and media orchestration (Firebase + Dropbox)
- Human-in-the-loop editing for controllable model output

## Key Capabilities

- Multi-channel prompt intake: typed prompts and voice transcription
- NER-driven content structuring with user-controlled refinement
- AI-guided visual generation with editable text/object layers
- Object replacement through inpainting flow
- One-click output rendering for square, portrait, and landscape formats
- Prompt history and reusable input patterns
- Authenticated user sessions (Google + email/password)

## System Workflow

1. User authenticates.
2. User optionally uploads source images with captions.
3. Prompt is submitted through text or voice.
4. NER response is reviewed and adjusted in a dynamic form.
5. Refined payload is transformed into an editable visual composition.
6. User performs object/text edits and optional inpainting.
7. Final creative is resized to target format and exported.

## Technical Stack

- Platform: Android (Kotlin)
- Auth/Data: Firebase Authentication, Realtime Database, Firestore, Storage
- Media Storage/Delivery: Dropbox API
- Networking: OkHttp
- Graphics/UI: AndroidSVG, Glide, Picasso, custom gesture controls
- AI Endpoints: transcription, NER, generation, inpainting, resizer

## Repository Structure

- `Android_Code/`: Android application source
- `Server_Code/`: model experimentation and API interaction notebooks
- `results/`: generated output samples
- `Weights/`: model assets and artifacts

## Quick Start

### Prerequisites

- Android Studio (latest stable)
- Firebase project
- Dropbox developer app
- Reachable AI service endpoints

### Setup

1. Clone repository:

```bash
git clone https://github.com/MuhammadAamirGulzar/vocalcraft-studio-ai.git
cd vocalcraft-studio-ai/Android_Code
```

2. Configure Firebase:

- Add Android app with package id `com.muhammadaamirgulzar.vocalcraft`
- Place `google-services.json` in `Android_Code/app/`
- Enable Authentication (Google, Email/Password) and Realtime Database

3. Configure Dropbox:

- Create scoped Dropbox app and grant required file/sharing permissions
- Update access token references in app code before local runs

4. Configure AI base URL:

- Update endpoint references if deploying outside the current service URL

5. Build and run from Android Studio.

## Security Notes

- Move all hardcoded keys and tokens to secure configuration before production deployment
- Route third-party API access through a protected backend where possible
- Apply principle-of-least-privilege for cloud credentials

## Licensing

MIT — see [LICENSE](LICENSE).

## Maintainer

- muhammadaamirgulzar



