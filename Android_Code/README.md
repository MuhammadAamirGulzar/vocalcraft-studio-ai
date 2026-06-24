# VocalCraft Studio - Android Module

This directory contains the Android client for VocalCraft Studio.

## Purpose

The mobile app delivers the full creative workflow:

- Prompt intake (voice/text)
- Structured AI refinement
- Visual generation and editing
- Multi-format export

## Build Targets

- `minSdk`: 24
- `targetSdk`: 34
- `compileSdk`: 34
- `applicationId`: `com.muhammadaamirgulzar.vocalcraft`

## Core Components

- Authentication screens and session routing
- Prompt and voice-transcription workflow
- NER validation/editing workflow
- Visual editor (`SvgActivity`) for object/text manipulation
- Export and upload pipeline

## Configuration Requirements

- Firebase project + `google-services.json`
- Dropbox app and access token
- Reachable AI API endpoints for transcription/NER/generation/inpainting/resizing

## Security Guidance

Before production usage:

- Remove hardcoded tokens from client code
- Move secrets and third-party credentials to secure backend services
- Enforce least-privilege access policies

## Reference

For product overview, architecture context, and complete setup instructions, use the repository root README.

