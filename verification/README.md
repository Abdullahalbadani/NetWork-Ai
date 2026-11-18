# Card studio client verification

This isolated branch checks the actual Network Copilot 0.9.0 client source using official Flutter 3.47.6/Dart3.13.5 and Gradle9.3.1 on a GitHub-hosted Linux runner. The conversation computer blocks Flutter's official download host, so this runner supplies the missing client analysis/build capability. It does not access the owner's Windows computer, Android phone, database or router.

The ZIP is a source-only verification fixture, not the project updater. It excludes local.properties, signing keys, private configuration, real databases, certificates, caches and build output. Font licenses accompany their fonts. The known R1 scrolling widget-test correction is included. No router credentials or production tokens are available to this workflow. Permissions are contents:read, checkout credentials are not persisted, third-party action and official Flutter source commits are pinned, and no APK is published or installed. The owner must still build with their existing local signing and perform physical acceptance.

The final update is prepared and tested separately against the confirmed0.8.2/schema5 baseline. This verification branch changes no default branch and is not a readiness claim before its checks finish.
