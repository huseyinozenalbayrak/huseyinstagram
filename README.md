# Huseyinstagram

A lightweight Instagram clone for iOS built with **Swift (UIKit)** and **Firebase**.  
It includes user authentication, feed display, photo upload with captions, and like functionality.

## ✨ Features
- 🔐 **Authentication** — Sign up, sign in, and sign out with Firebase Auth
- 🏠 **Feed** — Display posts with user email, image, caption, and like count
- ⬆️ **Upload** — Select an image, add a caption, and upload to Firebase Storage
- ❤️ **Likes** — Basic like functionality using Firestore
- ⚙️ **Clean structure** — Organized view controllers and reusable components
- 📦 **Dependency management** via CocoaPods

## 🧰 Tech Stack
- **Language:** Swift 5, UIKit  
- **Minimum iOS:** 13.0+  
- **Backend:** Firebase (Auth, Firestore, Storage)  
- **Dependency Manager:** CocoaPods  

## 📸 Screenshots
<p align="center">
  <img src="docs/screenshots/login.png" width="250" />
  <img src="docs/screenshots/feed.png"  width="250" />
  <img src="docs/screenshots/upload.png" width="250" />
</p>

## 🚀 Getting Started

### 1) Clone
```bash
git clone https://github.com/<your-username>/<your-repo>.git
cd <your-repo>
```

### 2) Firebase Setup

- Go to **Firebase Console** → Create a new project.  
- Add an iOS app with **Bundle ID = com.huseyinozenalbayrak.Huseyinstagram**
- Download the `GoogleService-Info.plist` file and add it to your **Xcode target**  
  (Make sure it appears in *Build Phases → Copy Bundle Resources*)
- Enable **Email/Password Authentication**
- Enable **Firestore** and **Storage**, and tighten rules as below:

#### Firestore Rules
```js
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write: if request.auth != null;
    }
  }
}
```

#### Storage Rules
```js
rules_version = '2';
service firebase.storage {
  match /b/{bucket}/o {
    match /{allPaths=**} {
      allow read, write: if request.auth != null;
    }
  }
}
```

> 💡 **Note:** `GoogleService-Info.plist` is not secret, but it is usually excluded from public repos.

### 3) Install Dependencies (CocoaPods)
```bash
sudo gem install cocoapods   # if not installed
pod install                  # Apple Silicon: arch -arm64 pod install
open Huseyinstagram.xcworkspace
```

### 4) Run the App
- Scheme: **Huseyinstagram**
- Device: iPhone Simulator or real device
- Build & Run (⌘R)

## 🧪 Project Structure
```
Huseyinstagram/
  ├─ AppDelegate.swift
  ├─ SceneDelegate.swift
  ├─ ViewController.swift
  ├─ FeedVC.swift
  ├─ UploadVC.swift
  ├─ SettingsVC.swift
  ├─ CustomCell.swift
  ├─ Assets.xcassets
  ├─ Main.storyboard
  └─ GoogleService-Info.plist  # (not tracked)
```

## 🔒 Security Checklist
- [ ] Firestore/Storage rules require authenticated users
- [ ] API key restricted by **API restrictions** and **Application restriction (iOS Bundle ID)**
- [ ] App Check enabled (optional but recommended)
- [ ] `GoogleService-Info.plist` is **ignored** in version control

## 🛠️ Useful Scripts
```bash
# Clean Pods and reinstall
pod deintegrate && rm -rf Pods Podfile.lock *.xcworkspace && pod install

# Clear DerivedData
rm -rf ~/Library/Developer/Xcode/DerivedData/*
```

## 🤝 Contributing
Pull requests are welcome. Please use the fork → feature branch → PR workflow.

## 📄 License
MIT
