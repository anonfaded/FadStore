# FadStore

Here’s the roadmap for building **FadStore**, step by step, ensuring we include GitHub metadata fetching, Firebase setup for reviews, and APK installation logic. Once finalized, I’ll convert this into a concise Markdown guide.

---

### **Roadmap: Building FadStore**

#### **1. Environment Setup**
1. Install **Android Studio** and set up an empty activity project.
2. Configure **Kotlin** as the programming language.
3. Set the package name to `com.fadedhood.fadstore`.

#### **2. Project Initialization**
1. **Dependencies**:
   - Add the following libraries to `build.gradle.kts`:
     ```gradle
     implementation "com.squareup.retrofit2:retrofit:2.9.0"
     implementation "com.squareup.retrofit2:converter-gson:2.9.0"
     implementation "com.github.bumptech.glide:glide:4.15.0"
     implementation "com.google.firebase:firebase-auth-ktx:22.0.0"
     implementation "com.google.firebase:firebase-firestore-ktx:25.0.0"
     ```
   - Sync your Gradle files.

2. **Project Structure**:
   - Create packages for:
     - `ui`: for activities and fragments.
     - `data`: for models and data classes.
     - `network`: for API calls.
     - `utils`: for helper classes.

#### **3. GitHub Metadata Setup**
1. **Admin Panel via GitHub**:
   - Create a dedicated GitHub repository for metadata.
   - Follow this structure:
     ```
     apps/
       app1/
         metadata.json
         icon.png
         screenshots/
       app2/
     ```
   - Example `metadata.json`:
     ```json
     {
       "name": "FadCam",
       "description": "Seamless background video recorder for Android – ad-free and open-source, with customizable options.",
       "apk_urls": {
         "arm64": "https://github.com/anonfaded/FadCam/releases/download/v1.2.1-beta/FadCam-v1.2.1-beta-arm64-v8a-release.apk",
         "armeabi": "https://github.com/anonfaded/FadCam/releases/download/v1.2.1-beta/FadCam-v1.2.1-beta-armeabi-v7a-release.apk",
         "universal": "https://github.com/anonfaded/FadCam/releases/download/v1.2.1-beta/FadCam-v1.2.1-beta-universal-release.apk",
         "x86": "https://github.com/anonfaded/FadCam/releases/download/v1.2.1-beta/FadCam-v1.2.1-beta-x86-release.apk",
         "x86_64": "https://github.com/anonfaded/FadCam/releases/download/v1.2.1-beta/FadCam-v1.2.1-beta-x86_64-release.apk"
       },
       "version": "1.0.0",
       "last_updated": "2025-01-15",
       "status": "active"
     }
     ```

2. **API Setup**:
   - Use the GitHub REST API for fetching metadata.
   - Implement a function to parse and store this metadata locally.

#### **4. Firebase Setup**
1. **Firebase Console**:
   - Create a project in the [Firebase Console](https://console.firebase.google.com).
   - Add your app to Firebase and download the `google-services.json` file.
   - Place `google-services.json` in the `app/` folder of your project.

2. **Firestore Database**:
   - Set up Firestore to store reviews, below is jsut dummy, actually user will have accounts:
     ```
     reviews/
       app1/
         user1: { "rating": 5, "review": "Great app!" }
     ```

3. **Authentication**:
   - Enable Email/Password authentication in Firebase.
   - Add Firebase authentication to the app for login/signup functionality.

#### **5. APK Installation Logic**
1. **Architecture Detection**:
   - Use `Build.SUPPORTED_ABIS` to detect the device architecture.
     ```kotlin
     val deviceArch = Build.SUPPORTED_ABIS[0]
     ```

2. **APK Selection**:
   - Fetch the compatible APK URL from the metadata.
   - Provide alternate links for manual selection.

3. **Download Manager**:
   - Use Android’s `DownloadManager` to handle APK downloads.
   - Prompt the user to install the APK after the download.

#### **6. UI/UX Design**
1. **Material Design 3**:
   - Use **Material Components** for consistent UI.
   - Dark mode (default) with AMOLED themes.
   - Tabs:
     - **Home**: List of apps with details and download options.
     - **Updates**: Show apps with pending updates.
     - **Account**: Manage user profile and reviews.

2. **Refresh and Auto-Fetch**:
   - Add a refresh button.
   - Use a background task to auto-fetch updates every minute.

#### **7. Notifications**
1. Implement Firebase Cloud Messaging (FCM) to notify users about updates or new apps.

#### **8. Testing**
1. Test on various devices for compatibility.
2. Ensure proper error handling for network issues or metadata inconsistencies.

---

### **Next Steps**
Let me know if this roadmap aligns with your vision, and I’ll refine the steps or convert this into a detailed Markdown file for GitHub. Once approved, we’ll start implementing step-by-step!