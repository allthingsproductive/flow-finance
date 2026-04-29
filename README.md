# flow. — Personal Finance Tracker (Firebase Edition)

## สิ่งที่ต้องทำก่อน deploy

### 1. สร้าง Firebase Project
1. ไปที่ console.firebase.google.com
2. "Create a project" → ตั้งชื่อ เช่น "flow-finance"
3. ปิด Google Analytics (ไม่จำเป็น)

### 2. เปิด Authentication
1. Build → Authentication → Get started
2. Sign-in method → Google → Enable → Save

### 3. สร้าง Firestore Database
1. Build → Firestore Database → Create database
2. Start in production mode → Next
3. เลือก region ใกล้สุด (asia-southeast1 = Singapore) → Done

### 4. ตั้ง Firestore Security Rules
Rules tab → แทนที่ด้วย:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users/{userId}/{document=**} {
      allow read, write: if request.auth != null && request.auth.uid == userId;
    }
  }
}
```
Publish

### 5. ใส่ Firebase Config ใน index.html
Project Settings (gear icon) → General → Your apps → Add app (</>) → Web
Copy firebaseConfig แล้วแทนที่ใน index.html บรรทัด YOUR_API_KEY ฯลฯ

### 6. Deploy ขึ้น Vercel
ตามขั้นตอนใน flow-deploy-guide.docx
