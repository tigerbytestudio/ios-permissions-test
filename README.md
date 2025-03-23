
# iOS Camera/Mic Permission Test Demo

This is a live demo to showcase a common issue developers face when implementing camera/microphone access in web applications — especially on **iOS Safari**.

🔗 **Live demo:**  
https://tigerbytestudio.github.io/ios-permissions-test/ios_webrtc_permission_demo.html

---

## 🔍 What This Demo Shows

This page contains two sections:

### ❌ Broken Version
- Uses `navigator.permissions.query({ name: "camera" })`
- **Fails on iOS Safari**, even when permissions are already granted
- Shows an "Access denied" message and alerts the user incorrectly

### ✅ Fixed Version
- Uses `navigator.mediaDevices.getUserMedia(...)`
- Works reliably on **iOS, Android, and desktop browsers**
- Displays live video feed and confirms camera/mic access

---

## 📱 Why This Happens on iOS Safari

iOS Safari enforces stricter rules:

- `navigator.permissions.query()` does **not return reliable results** for `camera` and `microphone`
- Access must come directly from a **user interaction**, like a button click
- Media access is only available in secure contexts (`https://`)

---

## ✅ Best Practice

Always use this pattern for requesting camera/mic access:

```js
async function getAccess() {
  try {
    const stream = await navigator.mediaDevices.getUserMedia({ video: true, audio: true });
    // Use the stream or preview it
  } catch (err) {
    alert("Access denied or failed: " + err.message);
  }
}
```

---

## 🧪 How to Test

1. Open the [demo page](https://tigerbytestudio.github.io/ios-permissions-test/ios_webrtc_permission_demo.html) in:
   - iOS Safari
   - Android Chrome
   - Desktop Chrome/Firefox

2. Tap both buttons:
   - The **broken version** should falsely show "Access denied"
   - The **fixed version** will prompt for permission and show your camera stream

---

## 🛠 Tech Stack

- Pure HTML + JavaScript
- GitHub Pages for HTTPS hosting

---

## 📂 File

- `ios_webrtc_permission_demo.html`: The complete HTML demo file

---

Created for client diagnostics and developer education around WebRTC and permissions on iOS.
