# Pre-Review Risk Checklist — VideoVault

> Generated for Phase 10 App Store preparation. Re-run grep before each submission.

**Scan date:** 2026-07-09  
**Scope:** `VideoVault/` source + `BackgroundInfo.plist` + in-app UI strings

---

## 1. Prohibited / placeholder text scan

| Pattern | Location | Risk | Status |
|---|---|---|---|
| `Video Master Pro` | `docs/PRD.md`, `docs/FEATURE_SCOPE.md` only | Low — internal docs, not shipped in app binary | ✅ Not in app target |
| `Coming Soon` | `docs/FEATURE_SCOPE.md` only | Low — documentation | ✅ Not in app UI |
| `TODO` / `FIXME` | None in `VideoVault/` | — | ✅ Clean |
| `example-w` | None in `VideoVault/` | — | ✅ Clean |
| `example.com` | None in `VideoVault/` | — | ✅ Clean |
| `Lorem ipsum` | None | — | ✅ Clean |
| `Pending configuration` | Removed | — | ✅ Replaced with "Available before launch" |

---

## 2. Invalid buttons / dead actions

| Item | Location | Risk | Status |
|---|---|---|---|
| Clear Cache | Removed in Phase 9 | — | ✅ Not present |
| Compress Video | Removed from Tools | — | ✅ Not in UI |
| Export (Coming Soon) | Removed from Tools | — | ✅ Not in UI |
| Privacy Policy link with fake URL | `AppLegalLinks` | Medium if example.com used | ✅ Uses nil URL + label |
| Terms of Use link with fake URL | `AppLegalLinks` | Medium | ✅ Uses nil URL + label |

---

## 3. Unimplemented features shown to users

| Feature shown | Actually implemented? | Notes |
|---|---|---|
| Import from Photos | ✅ | PhotosPicker + storage |
| Import from Files | ✅ | UIDocumentPicker |
| Playback / seek / speed | ✅ | AVPlayer |
| Playlists CRUD | ✅ | UserDefaults store |
| Background Playback | ✅ (Pro) | Audio session + background mode |
| Extract Audio | ✅ (Pro) | AVAssetExportSession |
| Add Background Music | ✅ (Pro) | VideoMixExportService |
| Adjust Volume | ✅ (Pro) | VideoMixExportService |
| Share | ✅ (Pro) | UIActivityViewController |
| Lifetime Pro IAP | ✅ | StoreKit 2 `videovault.pro.lifetime` |
| Compress Video | ❌ | ✅ Hidden — not shown |
| Record / camera | ❌ | ✅ Not in app |
| Cloud sync | ❌ | ✅ Not advertised in UI |

### Minor wording notes (low risk)

| Copy | Concern | Recommendation |
|---|---|---|
| "Advanced File Management" on Paywall | Vague marketing line | Acceptable — Share is Pro-gated; rename optional |
| "Unlimited Exports" on Paywall | No export limit enforced in code | Low risk — no hard cap exists |

---

## 4. Permissions audit

| Permission | In Info.plist? | Used? | Verdict |
|---|---|---|---|
| Photo Library (`NSPhotoLibraryUsageDescription`) | ✅ Added | Import from Photos | ✅ Required |
| Background audio (`UIBackgroundModes: audio`) | ✅ | Pro background playback | ✅ Required when feature enabled |
| Camera | ❌ | Not used | ✅ Correctly omitted |
| Microphone | ❌ | Not used | ✅ Correctly omitted |
| Location | ❌ | Not used | ✅ Correctly omitted |
| Tracking (`NSUserTrackingUsageDescription`) | ❌ | Not used | ✅ Correctly omitted |
| Files / document picker | N/A (system picker) | Import from Files | ✅ No extra plist key needed |

---

## 5. App Store Connect gaps (action required before submit)

| Item | Status |
|---|---|
| Publish Privacy Policy URL | ⏳ Host `PRIVACY_POLICY_DRAFT.md`, set `privacyPolicyURLString` |
| Publish Terms URL | ⏳ Host `TERMS_DRAFT.md`, set `termsOfUseURLString` |
| Support URL | ⏳ Set `supportURLString` + App Store Connect field |
| Contact email in legal docs | ⏳ Replace `[YOUR_CONTACT_EMAIL]` |
| IAP created in App Store Connect | ⏳ Verify `videovault.pro.lifetime` |
| Screenshots | ⏳ Follow `SCREENSHOT_PLAN.md` |
| App Privacy questionnaire | ⏳ Declare no data collection / no tracking |

---

## 6. Residual risk summary

| Priority | Risk | Mitigation |
|---|---|---|
| **High** | Submitting with nil legal URLs while screenshots show paywall footer | Configure URLs before final screenshot capture and submission |
| **Medium** | Reviewer tests Pro tools without sandbox purchase | Include StoreKit / sandbox steps in Review Notes (`APP_STORE_METADATA.md`) |
| **Low** | Internal docs mention competitor name | Keep docs out of app bundle; never reference in UI |
| **Low** | Paywall feature list slightly marketing-heavy | Optional copy trim in `ProUnlockView` |

---

## Quick re-scan commands

```bash
rg -i "Video Master Pro|Coming Soon|TODO|FIXME|example\.com|Lorem ipsum" VideoVault/
rg "Pending configuration" VideoVault/
```

Expected: no matches in `VideoVault/` except intentional placeholders in comments if any.
