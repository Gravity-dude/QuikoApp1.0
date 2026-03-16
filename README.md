# ⚡ Quiko — Offline Voice Assistant for Android

## What It Does
Quiko runs silently in the background and wakes up only when you say **"Hey Quiko"**.
Everything runs 100% offline — no internet, no cloud, no accounts.

---

## Features
| Voice Command | Action |
|---|---|
| `Hey Quiko, set alarm at 7 AM` | Alarm fires at 7:00 AM |
| `Hey Quiko, alarm in 30 minutes` | Alarm fires in 30 min |
| `Hey Quiko, set alarm at 14:30` | 24-hour format supported |
| `Hey Quiko, turn on flashlight` | Torch turns on |
| `Hey Quiko, turn off the torch` | Torch turns off |
| `Hey Quiko, remind me to drink water at 3 PM` | Notification at 3 PM |
| `Hey Quiko, remind me to call dad in 2 hours` | Notification in 2 hours |
| `Hey Quiko, what time is it` | Speaks current time aloud |
| `Hey Quiko, cancel alarm` | Cancels pending alarm |
| `Hey Quiko, help` | Lists all commands |

---

## How to Build the APK

### Requirements
- [Android Studio](https://developer.android.com/studio) (free, ~1 GB)
- Java 8+ (bundled with Android Studio)
- Android device running Android 8.0+ (API 26+)

### Steps

1. **Open the project**
   - Launch Android Studio
   - Click `Open` and select the `QuikoApp` folder

2. **Sync Gradle** (internet needed once)
   - Studio will prompt "Gradle sync required" — click **Sync Now**
   - Wait ~2 minutes for dependencies to download

3. **Build the APK**
   - Menu: `Build → Build Bundle(s)/APK(s) → Build APK(s)`
   - Wait for the build to complete (1–3 minutes)
   - Click **"locate"** in the bottom popup  
     OR navigate to: `app/build/outputs/apk/debug/app-debug.apk`

4. **Install on your phone**
   - Connect phone via USB (enable USB debugging in Developer Options)
   - Click the green ▶ Run button in Android Studio  
     **OR** copy the APK to your phone and install manually:
     - Settings → Security → **Install unknown apps** → ON
     - Open the APK file on your phone

---

## First-Time Phone Setup (IMPORTANT for offline speech)

Quiko uses Android's built-in speech recognizer in offline mode.
For best results, pre-download the offline English language pack:

### Google Speech Services (most phones)
1. Settings → Apps → Google → App Details
2. Make sure microphone permission is granted
3. Settings → General Management → Language
4. Tap your language → Download the **offline** speech recognition pack

### Samsung / Bixby phones
1. Settings → General Management → Voice Input
2. Select **Google** as voice input
3. Download English offline pack

### Note
- First use may download the offline model (~50 MB) automatically
- After that, everything works with airplane mode ON

---

## Architecture

```
QuikoApp/
├── VoiceListenerService.java   ← Foreground service, always listening
├── CommandProcessor.java        ← NLP parser + command executor
├── AlarmReceiver.java           ← Fires alarm notifications + sound
├── ReminderReceiver.java        ← Fires reminder notifications
├── BootReceiver.java            ← Restarts service after phone reboot
├── DatabaseHelper.java          ← SQLite — stores all reminders
├── MainActivity.java            ← Dark-themed dashboard UI
├── Reminder.java                ← Data model
└── ReminderAdapter.java         ← RecyclerView list adapter
```

---

## Troubleshooting

**"Hey Quiko" not responding?**
- Make sure the toggle switch in the app is ON
- Check notification bar — "Quiko Assistant" notification should be visible
- Grant microphone permission: Settings → Apps → Quiko → Permissions → Microphone

**Alarm didn't fire?**
- Android 12+: Settings → Apps → Quiko → Alarms & Reminders → Allow
- Battery optimization: Settings → Battery → Quiko → Don't optimize

**Speech not recognized offline?**
- Settings → Apps → Google → Storage → Clear cache
- Re-download offline speech pack (see First-Time Setup above)

---

## Privacy
- No internet connection ever required after build
- No data leaves your device
- All reminders stored locally in SQLite
- Microphone used only by Android's on-device speech engine
