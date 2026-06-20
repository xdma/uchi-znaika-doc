---
title: "Google Play Data Safety — УчиЗнайка"
permalink: /data-safety/
---

# Google Play Data Safety Form — УчиЗнайка (com.lm.ck)

Step-by-step answers for **Play Console → App content → Data safety**.  
Based on code-verified data inventory as of June 2026.

---

## Section 1 — Data collection and security

### "Does your app collect or share any of the required user data types?"
✅ **Yes**

### "Is all of the user data collected by your app encrypted in transit?"
✅ **Yes** — Firebase and AdMob communicate exclusively over HTTPS/TLS.

### "Do you provide a way for users to request that their data is deleted?"
✅ **Yes** — Users can email shos.dima@gmail.com. Add this URL to the deletion request field:
> https://xdma.github.io/uchi-znaika-doc/privacy-policy/ (the page includes deletion instructions in section 9 / раздел 9).

---

## Section 2 — Data types

Work through each category. Tick only what is listed below — everything else is **No / Not collected**.

### Personal info
| Data type | Collected? | Notes |
|---|---|---|
| Name | ❌ No | Child name is stored locally on-device only; never transmitted |
| Email address | ❌ No | |
| User IDs | ❌ No | |
| Address | ❌ No | |
| Phone number | ❌ No | |
| Race and ethnicity | ❌ No | |
| Political or religious beliefs | ❌ No | |
| Sexual orientation | ❌ No | |
| Other personal info | ❌ No | |

### Financial info — ❌ None collected

### Health and fitness — ❌ None collected

### Messages — ❌ None collected

### Photos and videos — ❌ None collected

### Audio files — ❌ None collected

### Files and docs — ❌ None collected

### Calendar — ❌ None collected

### Contacts — ❌ None collected

### App activity
| Data type | Collected? | Notes |
|---|---|---|
| App interactions | ✅ **Yes** | Firebase Analytics: app_opened, screen_viewed, game_started, session_ended (game_id, scores, duration, difficulty), parent_gate_attempt, settings_changed (key only), time_limit_reached, play_all events |
| In-app search history | ❌ No | |
| Installed apps | ❌ No | |
| Other user-generated content | ❌ No | |
| Other actions | ❌ No | |

### Web browsing — ❌ None collected

### App info and performance
| Data type | Collected? | Notes |
|---|---|---|
| Crash logs | ✅ **Yes** | Firebase Crashlytics: stack traces, uncaught exceptions |
| Diagnostics | ✅ **Yes** | Crashlytics: device model, Android version, memory state |
| Other app performance data | ❌ No | |

### Device or other identifiers
| Data type | Collected? | Notes |
|---|---|---|
| Device or other IDs | ❌ No | AD_ID permission is **not declared** in AndroidManifest.xml |

---

## Section 3 — For each data type you marked Yes

For **App interactions** (Firebase Analytics):

| Question | Answer |
|---|---|
| Is this data collected, shared, or both? | **Collected** |
| Is this data processed ephemerally? | No — retained by Firebase per Google's retention settings |
| Is this data required or can users opt out? | Required (cannot be disabled in app; can be disabled in Google account settings at device level) |
| Why is this data collected? | **Analytics** |

For **Crash logs** (Firebase Crashlytics):

| Question | Answer |
|---|---|
| Is this data collected, shared, or both? | **Collected** |
| Is this data processed ephemerally? | No |
| Is this data required or can users opt out? | Required |
| Why is this data collected? | **App functionality** → Crash analytics |

For **Diagnostics** (Firebase Crashlytics):

| Question | Answer |
|---|---|
| Is this data collected, shared, or both? | **Collected** |
| Is this data processed ephemerally? | No |
| Is this data required or can users opt out? | Required |
| Why is this data collected? | **App functionality** → Crash analytics |

---

## Section 4 — Advertising ID

### "Does your app use the Advertising ID?"
❌ **No** — `com.google.android.gms.permission.AD_ID` is not declared in AndroidManifest.xml.

> Note for reviewer: AdMob is integrated but configured with `CHILD_DIRECTED_TREATMENT_TRUE` and `UNDER_AGE_OF_CONSENT_TRUE`, which disables personalised ads and Advertising ID usage per Google's family policies.

---

## Section 5 — Families Policy

### "Is your app primarily directed to children under 13?"
✅ **Yes**

### Target age group
Select: **Ages 5 and under** (or **Ages 5–8** — pick the range that matches your Play Console app category; the app is designed for 4–6 year olds)

### "Does your app include ads?"
✅ **Yes** — Google AdMob interstitials

### "Do the ads comply with Google Play's Families Ads policy?"
✅ **Yes** — Ads are: non-personalised, child-directed, G-rated, no data collection from children for advertising purposes, frequency-capped at 1 per 3 minutes.

---

## Summary checklist before submitting

- [ ] Privacy policy URL entered (GitHub Pages URL for `docs/privacy-policy.md`)
- [ ] Data deletion request URL or instructions entered
- [ ] "App interactions" ticked under App activity
- [ ] "Crash logs" ticked under App info and performance
- [ ] "Diagnostics" ticked under App info and performance
- [ ] All three marked as **Collected** (not shared with third parties directly by you)
- [ ] Advertising ID: **No**
- [ ] Families: **Yes, primarily directed to children**
- [ ] Ads present: **Yes**, compliant with Families Ads policy
- [ ] Form saved → click **Submit for review**

---

## Notes on AdMob test IDs

The current build still uses Google's test AdMob IDs:
- App ID: `ca-app-pub-3940256099942544~3347511713`
- Interstitial unit: `ca-app-pub-3940256099942544/1033173712`

**Before promoting to production release** (not required for internal testing):
1. Create a real AdMob account at admob.google.com
2. Create an app + interstitial ad unit
3. Replace both IDs in `app/build.gradle.kts` (lines marked with `TODO` comments)
4. Make sure to enrol the app in the AdMob Families programme for the Kids category
