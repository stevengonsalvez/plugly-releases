# Plugly Privacy Policy

Last updated: 9 November 2026

Plugly is published by SHOT Clubhouse Ltd ("we", "us"). This policy covers the Plugly desktop app and the Plugly mobile app (Android package and iOS bundle identifier `com.pluglyhq.plugly.mobile`). Contact: steve@shotclubhouse.com.

## Summary

- The mobile app pairs with your own desktop. Pairing does not require a Plugly account.
- The content of your session traffic between the phone and the desktop is encrypted end to end by the pairing layer. Push notifications are different: their text passes through our push gateway and Apple or Google in readable form (see Push notifications).
- The mobile app has an optional, experimental sign-in to a Plugly Hub that you configure yourself. It is off by default.
- The mobile app contains no analytics or usage tracking code. The desktop app can send anonymous usage events, described below.
- We do not sell data and do not use it for advertising.

## What the mobile app does with your data

- **Camera.** Used to scan the QR code that pairs your phone with your desktop.
- **Microphone.** Used for voice dictation. Dictation is transcribed by your paired desktop.
- **Photos.** Images you choose to attach are sent to your own paired desktop session.
- **Local network (iOS).** iOS asks for local network access so the app can reach your desktop on your local network.
- **Diagnostics.** The connection diagnostics screen builds a report that you can copy to the clipboard. In app versions that remove the Send diagnostics action, nothing is transmitted from that screen. Earlier versions showed a Send diagnostics action that submitted a redacted, size-limited report (host name, endpoint, versions, connection state and events, never terminal contents or credentials) only after you tapped it.

## Push notifications

Your phone obtains a push token from Google Firebase Cloud Messaging (Android) or Apple Push Notification service (iOS) and sends that token, with its platform, to your paired desktop. Your desktop creates the random device identifier when you pair; the phone does not choose it. Your desktop registers the token and identifier with our push gateway.

When a notification is sent, your desktop gives the gateway the whole notification, which includes:

- the notification title and body text;
- the agent state and the notification source;
- a worktree identifier and a pane key.

Titles and bodies can contain branch names, worktree names and the status of your coding agents (for example "feat/x - Claude finished"). The gateway forwards the title and body to Apple (iOS) or Google (Android) so they can be shown on your phone, so the gateway and Apple or Google can read that text.

## Other network requests the mobile app makes

- **Relay connections.** When your phone connects to your desktop through a relay instead of directly, the phone opens a WebSocket connection to a relay server whose address comes from your pairing information. The relay sees your IP address and connection details. The session content on that connection is end-to-end encrypted by the pairing layer.
- **Agent icons.** To draw some agent icons, the app asks Google's favicon service (`www.google.com/s2/favicons`) for the icon of the agent's website. That request sends your IP address and the agent's domain name to Google.
- **Updates.** On Android, the app checks for updates by calling the GitHub API for the `plugly-releases` repository. On iOS, it looks up the app version with Apple's iTunes lookup service. These requests expose your IP address to GitHub or Apple.
- **Network troubleshooting.** The in-app network troubleshooting check queries Google Public DNS (`dns.google`), which sees your IP address.
- **Plugly Hub (optional, experimental).** If you switch on the experimental Plugly Hub setting and enter a Hub URL, the app signs in to that Hub using a device sign-in code, then sends a bearer token and your Hub requests to that URL. The Hub URL must use HTTPS. The Hub is run by whoever operates the URL you enter, and its handling of your data is governed by that operator. The setting is off by default and the Hub screens are reachable only after you enable it. We found no build setting that hides this option in release builds, so it appears in Settings.

## Encryption

Session traffic between the mobile app and your desktop passes through a pairing-based end-to-end encryption layer that runs over the WebSocket connection. The underlying network connection can itself be unencrypted on some paths. The mobile app permits plain `ws://` and HTTP connections to devices on your local network on iOS and, on Android, allows cleartext traffic generally. On iOS it also permits plain HTTP to the address ranges `100.64.0.0/10` and `fd7a:115c:a1e0::/48` (used by Tailscale). On those paths an observer of your network can see connection metadata such as addresses and traffic volume, and the content protection comes from the pairing layer only. The update, favicon, DNS and Hub requests above use HTTPS.

## What the desktop app collects

The desktop app can send anonymous usage events (no content, no file paths, no IP address stored against a profile). This can be disabled in Settings, Privacy, or by setting `DO_NOT_TRACK=1` or `PLUGLY_TELEMETRY_DISABLED=1`.

## Where data goes

- Desktop anonymous usage analytics: PostHog Cloud.
- Push delivery: our push gateway, then Apple Push Notification service (iOS) or Google Firebase Cloud Messaging (Android).
- Mobile requests listed above: GitHub, Apple, Google, a relay server, and a Hub URL you choose.

## Sharing

We do not sell personal data and do not share it with third parties except the service providers listed above, who process it on our behalf.

## Retention and deletion

To have a push registration or other data tied to your device removed, email steve@shotclubhouse.com. Tell us which app and platform you use and roughly when you paired. The device identifier is created by your desktop and the mobile app does not show it, so we will tell you what we need to find the registration when you write. Desktop analytics data is kept for the retention period of our analytics provider.

## Children

Plugly is not directed at children under 13 and is intended for adults.

## Changes

We will update this page when our practices change and revise the date above.

## Contact

SHOT Clubhouse Ltd, steve@shotclubhouse.com
