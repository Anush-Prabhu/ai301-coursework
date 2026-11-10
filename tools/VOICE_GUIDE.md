# Voice guide copies (generated)

**Source of truth:** `C:\Users\anush\.claude\voice-guard\voice-guide.md`

The `voice-guide.md` files under `repro-check/`, `plan-check/`, and `pr-precheck/` are copies, not independently edited files. Windows on this machine cannot create symlinks for the skill folders, so the copies are refreshed from the canonical guide:

```powershell
powershell -NoProfile -File $env:USERPROFILE\.claude\voice-guard\refresh_voice_guides.ps1
```

Do not hand-edit the copies; change the canonical file, then refresh.
