# Firebase Setup Checklist

You're getting "Invalid credentials" because the user doesn't exist in Firebase yet.

## ✅ Quick Setup (Follow in Order)

### Step 1: Enable Firestore Database
1. Go to: https://console.firebase.google.com/project/harrep/firestore
2. Click **"Create database"**
3. Choose **"Start in production mode"**
4. Select location (e.g., us-central)
5. Click **"Enable"**
6. Wait for it to finish

### Step 2: Set Firestore Rules
1. Click the **"Rules"** tab
2. Delete everything and paste this:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /reports/{reportId} {
      allow create: if true;
      allow read, update, delete: if request.auth != null;
    }
  }
}
```

3. Click **"Publish"**

### Step 3: Enable Authentication
1. Go to: https://console.firebase.google.com/project/harrep/authentication
2. Click **"Get started"**
3. Click **"Email/Password"** in the list
4. Toggle **"Enable"** to ON
5. Click **"Save"**

### Step 4: Create Admin User ⚠️ THIS IS WHY YOU'RE GETTING THE ERROR
1. Still in Authentication, click **"Users"** tab
2. Click **"Add user"** button
3. Enter:
   - **Email**: `testuser@123`
   - **Password**: `user@123`
4. Click **"Add user"**
5. **COPY THE USER UID** (the long string like "abc123xyz...")

### Step 5: Set Admin Privileges
1. Open your terminal in the project folder
2. Run:
```bash
npm install firebase-admin
```

3. Open `set-admin.js` file
4. Find line 15: `const uid = 'PASTE_USER_UID_HERE';`
5. Replace `PASTE_USER_UID_HERE` with the UID you copied in Step 4
6. Save the file
7. Run:
```bash
node set-admin.js
```

You should see: "✅ SUCCESS! Admin claim set successfully!"

### Step 6: Test Login
1. Open `admin.html` in your browser
2. Enter:
   - Email: `testuser@123`
   - Password: `user@123`
3. Click **Login**

You should now be able to login!

## 🔍 Current Status Check

Run these checks:

**Check 1: Is Firestore enabled?**
- Go to: https://console.firebase.google.com/project/harrep/firestore
- You should see a database, not a "Create database" button

**Check 2: Is Authentication enabled?**
- Go to: https://console.firebase.google.com/project/harrep/authentication
- You should see "Email/Password" as "Enabled"

**Check 3: Does the user exist?**
- Go to: https://console.firebase.google.com/project/harrep/authentication/users
- You should see `testuser@123` in the list

**Check 4: Does the user have admin claim?**
- After running `set-admin.js`, you should see success message

## 🆘 Still Not Working?

If you're still getting "Invalid credentials":

1. **Double-check the email**: Must be exactly `testuser@123`
2. **Double-check the password**: Must be exactly `user@123`
3. **Check browser console**: Press F12 and look for error messages
4. **Verify user exists**: Go to Firebase Console → Authentication → Users
5. **Try creating user again**: Delete the old user and create a new one

## 📸 Visual Guide

### Where to find things in Firebase Console:

1. **Firestore Database**: Left menu → Firestore Database
2. **Authentication**: Left menu → Authentication
3. **Add User**: Authentication → Users tab → "Add user" button
4. **User UID**: In the Users list, click on the user to see the UID

---

**Need help?** Check the browser console (F12) for detailed error messages.
