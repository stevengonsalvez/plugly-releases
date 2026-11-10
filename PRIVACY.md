# Plugly Privacy Policy

Last updated: 11 November 2026

Plugly is published by SHOT Clubhouse Ltd ("we", "us"). This policy covers the Plugly desktop app and the Plugly mobile app (Android package and iOS bundle identifier `com.pluglyhq.plugly.mobile`). Contact: steve@shotclubhouse.com.

## Current status of Plugly servers

No Plugly-operated push gateway or relay is running yet. Shipped desktop builds point at a placeholder address that does not resolve, so notifications are not delivered through any Plugly server and we hold no push registrations, unless you configure your own gateway. The desktop's default relay address is also a placeholder that does not resolve, so the desktop does not reach a Plugly relay either. Feedback and diagnostic uploads from the desktop, the desktop's update nudge and changelog checks, and its connector address also point at placeholder addresses that do not resolve, so we receive none and nothing is sent to us. We will update this policy when a Plugly gateway or relay goes live, and the sections below say what would then be sent.

## Summary

- The mobile app pairs with your own desktop. Pairing does not require a Plugly account.
- Connections between the phone and the desktop that are built on the pairing encryption layer use it to protect session content end to end. Not every path is covered, see Encryption. Push notifications are different: if a gateway is used, their text and several identifiers, including your local folder path, pass through that gateway and Apple or Google in readable form (see Push notifications).
- The mobile app has an optional, experimental sign-in to a Plugly Hub that you configure yourself. It is off by default.
- The mobile app has no analytics of its own. On Android, Google's ML Kit (QR scanning, on-device dictation) and Firebase Cloud Messaging libraries send Google device and app information, per-install identifiers and performance data. The desktop app can send anonymous usage events, described below.
- We do not sell data and do not use it for advertising.

## What the mobile app does with your data

- **Camera.** Used to scan the QR code that pairs your phone with your desktop. On Android, the scanning uses Google ML Kit libraries bundled in the app.
- **Microphone.** Used for voice dictation. Dictation is transcribed on your phone or on your paired desktop. On iOS the phone uses Apple's speech recognition built into the operating system. On Android the app tries Google ML Kit first, which is a library inside the app and not part of the operating system, and then Android's on-device recognizer. Language assets may be downloaded from Apple or Google. On the desktop, if you choose an OpenAI transcription model and supply your own OpenAI API key, the desktop may send the recorded audio to OpenAI, which handles it under its own policy.
- **Photos and files.** Images you choose to attach, and any file you pick with the file picker, are sent to your own paired desktop session. When you save an image from a session, the app adds it to Photos using add-only access, which does not let the app read your library.
- **Clipboard.** When you paste into a session, the app reads your clipboard and sends the pasted text or image to your paired desktop.
- **Local network (iOS).** iOS asks for local network access so the app can reach your desktop on your local network.
- **Diagnostics.** The connection diagnostics screen builds a report that you can copy to the clipboard. Current versions do not show a Send diagnostics action, so nothing is transmitted from that screen. Earlier versions showed a Send diagnostics action that, after you tapped it, attempted to submit a redacted, size-limited report (host name, endpoint, versions, connection state and events, never terminal contents or credentials). The address that action used did not resolve, so those reports were attempted but none were received by us.

## Push notifications

On iOS, your phone obtains a push token from Apple Push Notification service and sends that token, with its platform, to your paired desktop. On Android, push needs a real Firebase configuration, which current builds do not include, so Android push does not work and no token is obtained in current builds. When push is configured, the phone gets a token from Google Firebase Cloud Messaging and sends it, with its platform, to your paired desktop. Your desktop creates the random device identifier when you pair; the phone does not choose it.

Notifications only travel through a push gateway if your desktop is configured with one. Shipped desktop builds default to a placeholder gateway address that does not resolve, so unless you set your own https gateway address (the `PLUGLY_PUSH_GATEWAY_URL` setting), your token is not registered anywhere and no notification leaves your desktop for a gateway.

If you configure a gateway, your desktop registers the token and device identifier with it. When a notification is sent, your desktop gives that gateway the whole notification, which includes:

- the notification title and body text;
- the agent state and the notification source;
- a worktree identifier, which is built from the repository identifier and the absolute path of the worktree folder on your computer, so it usually contains your computer's folder names and often your operating system user name;
- a pane key, the execution host, an identifier (fingerprint) of your desktop, and notification identifiers and counters.

Titles and bodies can contain branch names, worktree names and the status of your coding agents (for example "feat/x - Claude finished"). The gateway forwards the title and body to Apple (iOS) or Google (Android) so they can be shown on your phone. It also includes the other fields above, including the worktree identifier and its folder path, in the data it sends to Apple or Google with the notification. The gateway operator and Apple or Google can therefore read that text and those identifiers. If we run a gateway in future, we will name the operator and retention in an updated policy.

## Other network requests the mobile app makes

- **Relay connections.** When your phone connects to your desktop through a relay instead of directly, the phone opens a WebSocket connection to a relay server whose address comes from your pairing information. No Plugly relay is running today, so this only happens if your pairing information points at a relay run by you or someone else. The relay sees your IP address and connection details. Session content on that connection is protected by the pairing layer where the connection is built on it (see Encryption).
- **Agent icons.** To draw some agent icons, the app asks Google's favicon service (`www.google.com/s2/favicons`) for the icon of the agent's website. That request sends your IP address and the agent's domain name to Google.
- **Images and avatars.** Images shown in chats can be loaded from any web address (http or https) that appears in the conversation, and the host serving the image sees your IP address. The same applies to https images in pull request, issue and task text, to comment author avatars in pull request views, and to repository icons whose image comes from a web address supplied by your desktop, such as a favicon service or a GitHub avatar address. Web-based screens inside the app allow any https image.
- **Google libraries on Android.** The Android app includes Google's ML Kit (QR scanning and on-device dictation) and Firebase Cloud Messaging libraries. Per Google's own documentation these send Google device and app information, per-install identifiers (such as a Firebase installation ID), performance metrics, event types and error codes for diagnostics and usage analytics. This is Google's data collection under Google's policies; we do not receive it.
- **Updates.** On Android, the app checks for updates by calling the GitHub API for the `plugly-releases` repository, and its update action opens a GitHub release page. On iOS, it looks up the app version with Apple's iTunes lookup service. These requests expose your IP address to GitHub or Apple.
- **Network troubleshooting.** The in-app network troubleshooting check queries Google Public DNS (`dns.google`), which sees your IP address.
- **Plugly Hub (optional, experimental).** If you switch on the experimental Plugly Hub setting and enter a Hub URL, the app signs in to that Hub using a device sign-in code, then sends a bearer token and your Hub requests to that URL. The Hub URL must use HTTPS. The Hub is run by whoever operates the URL you enter, and its handling of your data is governed by that operator. The setting is off by default and the Hub screens are reachable only after you enable it. We found no build setting that hides this option in release builds, so it appears in Settings.

## Encryption

Session traffic between the mobile app and your desktop can pass through a pairing-based end-to-end encryption layer. We verified that the mobile app's WebSocket session client to your desktop performs the paired encryption handshake (legacy and v2) before session content is exchanged. We have not verified every other connection type, so connections that are built on the paired encryption layer use it, and we make no end-to-end claim for others. The underlying network connection can itself be unencrypted on some paths. The mobile app permits plain `ws://` and HTTP connections to devices on your local network on iOS and, on Android, allows cleartext traffic generally. On iOS it also permits plain HTTP to the address ranges `100.64.0.0/10` and `fd7a:115c:a1e0::/48` (used by Tailscale). On those paths an observer of your network can see connection metadata such as addresses and traffic volume, and the content protection comes from the pairing layer only. The update, favicon, DNS and Hub requests above use HTTPS. Image and avatar addresses may be plain HTTP if the address itself is.

## What the desktop app collects and sends

- **Anonymous usage events.** The desktop app can send anonymous usage events (no content, no file paths, no IP address stored against a profile) to PostHog Cloud. This can be disabled in Settings, Privacy, or by setting `DO_NOT_TRACK=1` or `PLUGLY_TELEMETRY_DISABLED=1`.
- **Feedback.** If you submit feedback from the app, the desktop posts your feedback text, your GitHub login and email if available, the app version and operating system details, and optionally a diagnostic bundle and images you attach. This only happens when you submit. The address built into current builds is a placeholder that does not resolve, so we do not receive these submissions today.
- **Diagnostic bundle upload.** If diagnostic sending is enabled, you can upload a diagnostic bundle after a confirmation dialog. Release builds are built with an upload address that is a placeholder and does not resolve, so we do not receive these uploads today.
- **Speech models.** When you download a local speech model, the desktop downloads it from `huggingface.co`, which sees your IP address.
- **Browser extensions.** The embedded browser's Chrome extension update checks go to `update.googleapis.com`.
- **Integrations you connect.** If you connect services such as GitHub, GitLab, Linear, Jira (through `api.atlassian.com`), OpenAI, Anthropic or Google, the desktop sends requests to them with the credentials you provide, and they handle that data under their own policies.
- **Cloud sign-in.** The desktop app contains support for a Plugly cloud sign-in using OpenID Connect that would request your profile, your email address and offline access (a refresh token). It is not yet available: it targets a placeholder address and cannot complete.

## Where data goes

- Desktop anonymous usage analytics: PostHog Cloud.
- Push delivery: only if you configure a gateway, then that gateway, then Apple Push Notification service (iOS) or Google Firebase Cloud Messaging (Android). Today no Plugly gateway receives anything.
- Mobile requests listed above: GitHub, Apple, Google, OpenAI (desktop dictation only, if you configure it), a relay server if your pairing information points at one, any host serving an image or avatar, and a Hub URL you choose.
- Desktop requests listed above: PostHog, Hugging Face, Google, and the services you connect.

## Sharing

We do not sell personal data. Services named in this policy, including Apple, Google (including ML Kit and Firebase), GitHub, PostHog, OpenAI, Hugging Face, any relay or push gateway operator, any Hub operator and any host that serves an image, are third parties (and, once one is running, the Plugly gateway operator named in an updated policy). They handle data under their own policies, and we do not control them, except where an updated policy says otherwise for a Plugly-operated service.

## Retention and deletion

We hold no push registrations today because no Plugly gateway is running, so there is nothing of that kind for us to delete. If a Plugly gateway goes live and you want a push registration or other data tied to your device removed, email steve@shotclubhouse.com. The device identifier is created by your desktop and the mobile app does not show it, so we will tell you what we need to find the registration when you write. Desktop analytics data is kept for the retention period of our analytics provider.

## Children

Plugly is not directed at children under 13 and is intended for adults.

## Changes

We will update this page when our practices change, including when a Plugly push gateway or relay goes live, and revise the date above.

## Contact

SHOT Clubhouse Ltd, steve@shotclubhouse.com
