# 📤 ShareSheet2OCI: Upload Files to OCI Object Storage via iOS Share Sheet

**Seamlessly upload files/videos/images from your iOS device to Oracle Cloud Infrastructure (OCI) Object Storage using a Pre-Authenticated Request (PAR).**  
This shortcut leverages iOS Shortcuts’ Share Sheet integration for one-tap uploads—perfect for photos, documents, and more!

---

## 🚀 Features
- **Direct Share Sheet Integration**: Upload files/videos/images directly from **→any iOS app←** 📱.
- **No Coding Required**: Uses OCI’s Pre-Authenticated Requests for secure uploads.
- **Bulk Upload Support**: Handles multiple files at once.
- **Custom Notifications**: Get confirmation when uploads succeed.

---

## 📋 Prerequisites
1. An **OCI Bucket** configured in your Oracle Cloud account.
2. **iOS Shortcuts App** installed on your device (iOS 13+).

---

## 🛠️ Setup Guide

### Step 1: Create a Pre-Authenticated Request (PAR) in OCI
1. **Navigate to your OCI Bucket**  
   - Open the [OCI Console](https://cloud.oracle.com/).
   - Go to **Storage > Buckets** and select your target bucket.

2. **Generate a PAR**  
   - Click **Create Pre-Authenticated Request**.
   - Configure settings as follows:  
     | Field                 | Value                                  |
     |-----------------------|----------------------------------------|
     | Name                  | `PAR-Uploader-iOS` (or a custom name)  |
     | Target                | `Bucket` (default)                    |
     | Access Type           | **Permit object reads and writes**    |
     | Enable Object Listing | ✔️ Enabled                            |
     | Expiration            | Set a long-term date (e.g., 12/31/9999) |
   - **Copy the generated PAR URL** (you’ll need this for the shortcut).

   ![PAR Configuration Example](https://github.com/user-attachments/assets/c2ae7462-58fd-4422-8c7c-9fa06709d520)

---

### Step 2: Build the iOS Shortcut
1. **Create a New Shortcut**  
   - Open the **Shortcuts App** → Tap **+** → Name it (e.g., `ShareSheet2OCI`).

2. **Enable Share Sheet Access**  
   - Tap the **⚙️ Settings (ⓘ)** → Enable **Show in Share Sheet**.
   - Choose supported file types (All file types enabled by default ✅).

3. **Add Actions**  
   Follow the workflow below or [**Download the Shortcut**](https://www.icloud.com/shortcuts/c70bb1b234064b04bfa2969eb60a82d4) directly.

   ```markdown
   1. Receive [Input] from Share Sheet
   2. Search Action [Repeat with Each] -> Repeat with Each Item in [Shortcut Input]
      └─ 3. Search Action [Get Details of Files] -> Get Name of [Repeat Item]
      └─ 4. Search Action [URL Encode] -> URL Encode the filename
      └─ 5. Search Action [Text] -> Text: Combine PAR URL + Encoded Filename  
         (Example: `https://<PAR_URL>/` + `EncodedText` → **NO SPACE**)
      └─ 6. Search Action [Get Contents of URL] -> Upload File via PUT Request  
         - Method: **PUT**  
         - Headers: None  
         - Request Body: **File** (select "Repeat Item")
      └─ 7. (Optional) Search Action [Show Notification] -> Show Notification on Success
   ```
   ![image](https://github.com/user-attachments/assets/18e07ebb-3ff4-4c92-852a-b83292427fdf)


