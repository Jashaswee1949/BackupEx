# BackupEx

[![Platform](https://img.shields.io/badge/Platform-Android%208.0%2B%20(API%2026%2B)-green.svg)](https://android.com)
[![Language](https://img.shields.io/badge/Language-Kotlin%202.2-blue.svg)](https://kotlinlang.org)
[![UI](https://img.shields.io/badge/UI-Jetpack%20Compose-purple.svg)](https://developer.android.com/jetpack/compose)
[![Privacy](https://img.shields.io/badge/Privacy-100%25%20Offline%20(No%20Internet)-brightgreen.svg)]()
[![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

**BackupEx** is a high-performance, fully offline Android application that decrypts WhatsApp end-to-end encrypted backup files (`.crypt15`, `.crypt14`) directly on-device and provides an authentic WhatsApp-style AMOLED chat viewer.

Designed to navigate large conversation histories with responsive message loading, fast full-text & date search, and quoted reply navigation.

---

## âœ¨ Features

- ðŸ”’ **100% Offline & Private:**
  - **Zero network permissions** (`INTERNET` permission is completely absent from the manifest).
  - Decryption, database indexing, and chat rendering are executed entirely on-device. No data or telemetry ever leaves your phone.
- ðŸ’¬ **WhatsApp AMOLED Chat Experience:**
  - Modern, true-black AMOLED theme (`#000000`) with authentic WhatsApp dark green accents and message bubble styling.
  - Displays outgoing/incoming bubbles, delivery ticks, timestamps, sender names in groups, and media type placeholders (Photos, Videos, Audio, Voice Notes, Documents, Stickers, Locations, and Contacts).
- ðŸ“œ **Efficient Keyset Pagination:**
  - Powered by AndroidX **Paging 3** with indexed SQLite keyset queries.
  - Loads messages in small, bounded batches on demand, avoiding loading entire chat histories into memory.
- ðŸ” **Fast Text & Date Search:**
  - Debounced substring search across conversations.
  - Multi-language search support (including English, Hinglish, Hindi, Odia, and emojis).
  - Date search parsing (e.g., jump directly to `2 Nov 2022`).
- â†©ï¸ **WhatsApp Quoted Reply Navigation:**
  - Tap on quoted replies inside message bubbles to immediately jump to and highlight the referenced messageâ€”even if it is unloaded and further back in the chat.
- âš¡ **Offline Decryption Engine:**
  - Embedded Python runtime powered by **Chaquopy** and `wa-crypt-tools`.
  - Supports WhatsApp 64-hex-digit encryption keys with `.crypt15` and `.crypt14` backups.
- ðŸª¶ **Optimized & Lightweight:**
  - ProGuard and R8 full code shrinking and resource stripping.
  - Single-architecture (`arm64-v8a`) native library packaging producing an ultra-compact ~13.3 MB release APK.

---

## ðŸ› ï¸ Tech Stack & Architecture

- **Language:** Kotlin 2.2
- **UI Framework:** Jetpack Compose with Material 3 (AMOLED Dark Palette)
- **Architecture:** MVVM (Model-View-ViewModel) + Repository Pattern
- **Pagination:** AndroidX Paging 3 (Keyset / ID & Timestamp pagination)
- **Database:** SQLite / Android SQLiteOpenHelper
- **Decryption:** [Chaquopy](https://chaquo.com/chaquopy/) (Python 3.10 for Android) + `wa-crypt-tools`
- **Build System:** Gradle 9.8.2 + Android Gradle Plugin 9.5.0
- **Min SDK:** Android 8.0 (API 26) | **Target SDK / Compile SDK:** API 37

---

## ðŸš€ Getting Started

### Prerequisites

- [Android Studio Ladybug | 2024.2+](https://developer.android.com/studio) or newer
- **Java 25** (Configured via Gradle Daemon toolchain in `gradle/gradle-daemon-jvm.properties`; automatically downloaded by the Foojay toolchain resolver in `settings.gradle.kts`, or provided by your IDE's bundled JBR 25)
- **Android SDK** (Compile SDK / Target SDK: API 37, Min SDK: API 26)

### Building from Source

1. **Clone the repository:**
   ```bash
   git clone https://github.com/<your-username>/BackupEx.git
   cd BackupEx
   ```

2. **Open in Android Studio:**
   - Open Android Studio, select **Open**, and choose the `BackupEx` folder.
   - Wait for Gradle sync to complete.

3. **Build the Release APK:**
   ```bash
   ./gradlew assembleRelease
   ```
   The optimized release APK will be generated at:
   `app/build/outputs/apk/release/app-release.apk`

---

## ðŸ“– How to Use

1. **Export / Locate your WhatsApp Backup:**
   - Locate your WhatsApp encrypted database (e.g., `msgstore.db.crypt15`) on your device storage (commonly found in `Android/media/com.whatsapp/WhatsApp/Databases/`).
2. **Obtain your 64-digit Encryption Key:**
   - If End-to-End Encrypted Backups are enabled in WhatsApp: *Settings -> Chats -> Chat Backup -> End-to-End Encrypted Backup*.
3. **Import into BackupEx:**
   - Launch BackupEx.
   - Enter the full path to your `.crypt15` file and paste your 64-digit hex encryption key.
   - Tap **Decrypt & Import**.
4. **Browse & Search:**
   - Once decrypted, your full chat list will be loaded. Tap any chat to read messages, search history, or jump to specific dates.

---

## ðŸ” Privacy & Security

BackupEx is engineered strictly as a read-only offline backup viewer:
- **No Internet Access:** The application does not declare `android.permission.INTERNET`. It cannot connect to any external server or network.
- **No Live WhatsApp Interactivity:** Does not interface with your active WhatsApp account or servers; reading backups will never trigger read receipts (blue ticks) or affect your live account.
- **Local Storage:** Decrypted databases remain strictly inside the app's protected private sandboxed storage directory.

---

## ðŸ‘¤ Author

Developed with care by **Jashaswee**.

---

## ðŸ“„ License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.