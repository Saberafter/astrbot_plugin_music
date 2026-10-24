# Fork Scope

- This is a maintenance fork of `Zhalslar/astrbot_plugin_music`.
- Keep author attribution and the MIT license.
- `main` tracks upstream. Custom changes belong to `codex/onebot-direct-audio`.
- Before any manual or automatic upgrade, remind the maintainer to merge upstream into the custom branch.
- Never force-sync the custom branch with upstream or overwrite it with marketplace code.
- Preserve direct OneBot sending for both local audio and URL fallback.
- Local file URIs require the OneBot peer to see the same absolute path.
- Keep the generic `Record` behavior unchanged for other platforms.
- Keep `metadata.yaml` and AstrBot's persisted install source pointing to this fork.
- Prefer small changes without new dependencies or unrelated refactors.
- Do not run automated tests or send test songs unless explicitly requested.
- Never commit deployment configuration, credentials, logs, or downloaded audio.
