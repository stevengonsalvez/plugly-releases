# Plugly Privacy Policy

Last updated: 9 November 2026

Plugly is published by SHOT Clubhouse Ltd ("we", "us"). This policy covers the Plugly desktop app and the Plugly mobile app (Android package and iOS bundle identifier `com.pluglyhq.plugly.mobile`). Contact: steve@shotclubhouse.com.

## Summary

- Plugly has no account system. We do not collect your name, email address, phone number, location, contacts or payment details.
- The mobile app talks to your own paired desktop. Terminal content, prompts, files and repository data stay between your phone and your computer and are not sent to us.
- The mobile app contains no analytics or usage tracking and sends no diagnostics to us.
- To deliver push notifications, a push token and a random device identifier are registered with our push gateway. The desktop app can send anonymous usage events, described below.
- We do not sell data and do not use it for advertising.

## What the mobile app does with your data

- **Camera.** Used to scan the QR code that pairs your phone with your desktop.
- **Microphone.** Used for voice dictation. Dictation is transcribed by your paired desktop.
- **Photos.** Images you choose to attach are sent to your own paired desktop session.
- **Push notifications.** Your phone obtains a push token from Google Firebase Cloud Messaging (Android) or Apple Push Notification service (iOS) and sends that token, with its platform, to your paired desktop. The random device identifier is created by your desktop when you pair; the phone does not choose it. Your desktop registers the token and identifier with our push gateway, which uses them only to deliver the notifications you have enabled.
- **Diagnostics.** The connection diagnostics screen builds a report that you can copy to the clipboard. The app does not transmit it anywhere. Anything you paste or share from there is your choice.
- **Other network requests the app makes itself.** On Android, the app checks for updates by calling the GitHub API for the `plugly-releases` repository. On iOS, it looks up the app version with Apple's iTunes lookup service. The in-app network troubleshooting check queries Google Public DNS (`dns.google`). These requests carry no Plugly account data because Plugly has no accounts.

## What the desktop app collects

The desktop app can send anonymous usage events (no content, no file paths, no IP address stored against a profile). This can be disabled in Settings, Privacy, or by setting `DO_NOT_TRACK=1` or `PLUGLY_TELEMETRY_DISABLED=1`.

## Where data goes

- Desktop anonymous usage analytics: PostHog Cloud.
- Push delivery: our push gateway, then Google Firebase Cloud Messaging (Android) or Apple Push Notification service (iOS).
- Connections between your phone and your desktop are encrypted in transit.

## Sharing

We do not sell personal data and do not share it with third parties except the service providers listed above, who process it on our behalf.

## Retention and deletion

To have a push registration or other data tied to your device removed, email steve@shotclubhouse.com and describe your device. Desktop analytics data is kept for the retention period of our analytics provider.

## Children

Plugly is not directed at children under 13 and is intended for adults.

## Changes

We will update this page when our practices change and revise the date above.

## Contact

SHOT Clubhouse Ltd, steve@shotclubhouse.com
