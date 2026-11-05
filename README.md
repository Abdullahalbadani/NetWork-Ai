# Network Copilot 0.6 delivery

This branch contains the tested update package for the existing Windows project at `D:\NetWork-Ai`. It is a code delivery package.

Archive: [copilot-foundation-v0.6.zip](deliveries/v0.6/copilot-foundation-v0.6.zip)

ZIP SHA256:

```text
d36e82adb40155a3574cf918d418ffdc611c66046f557817a3240caaf055dcdd
```

1. Download the archive with GitHub's download button and save it to your desktop.
2. Stop the existing Flutter process and Node server.
3. Verify the ZIP hash, then extract into a new folder, for example `D:\copilot-update-v06`.
4. Run `node "D:\copilot-update-v06\install.cjs" "D:\NetWork-Ai"`.
5. Keep the printed code backup path. Follow `D:\NetWork-Ai\docs\foundation-windows.md` for Docker, owner setup, TOTP, certificates, CHR import, Chrome and USB Android testing.

The installer validates the unchanged frozen update, refuses unknown file edits and preserves private configuration. It does not start services.

The archive contains source updates, a portable Node runtime and new Flutter cache packages. No user credentials, `.env`, Google API key, private configuration or router passwords are included.

Backend tests: 61 passed. Flutter tests: 33 passed. Physical Windows/CHR/Gemini/Android acceptance remains required. The cloud APK build was blocked by an HTTP 403 policy denial for a Flutter dependency.

## Setup diagnostics update 0.6.1

A small tested setup-diagnostics update is in `deliveries/v0.6/copilot-setup-diagnostics-v0.6.1.zip`.

ZIP SHA256: `329b0f2b793607c0c30c7d26e0bbe825830abcd07de19d21596c56ff3e9540ad`

Extract into `D:\copilot-setup-diagnostics-v061` and run `node "D:\copilot-setup-diagnostics-v061\install.cjs" "D:\NetWork-Ai"`. Then retry normal owner setup. Send only the bounded `Setup diagnostic:` line if it fails.

This update reports setup stage and known error/exit codes without raw error messages or private state. Windows private-directory grants use numeric token/SYSTEM SIDs. The root cause on the actual Windows computer is still being diagnosed. The update preserves private files and does not start or alter Docker containers while applying.
