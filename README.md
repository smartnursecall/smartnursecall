# Smart NurseCall

A **Real-Time Nurse Call Management System** designed for healthcare facilities. The system is integrated with **Firebase Realtime Database** to deliver instant notifications to nurses, enabling quick responses to patient requests. It focuses on a responsive interface, simple workflows, and secure data handling.

## Features

- **Real-Time Dashboard:** Displays active and handled calls with live updates, no page refresh required.  
- **Colored Priority Indicators:** Each call is marked with a distinct color (Red for Medical, Yellow for Infusion, Green for Non-Medical) to simplify priority identification.  
- **Call History:** A complete archive table of all handled calls, with date-based filtering and the ability to delete data by date.  
- **Customizable Settings:** Users can enable/disable sound notifications, browser notifications, and switch between Light Mode and Dark Mode.  
- **User Management:** Includes login and logout pages to ensure only authorized staff can access the dashboard.  
- **Clear Status Button:** Removes all handled calls from the active view.  
- **Responsive Interface:** Layout optimized for desktop, tablet, and mobile devices.  

## Architecture

- **Front-end:** Pure HTML, CSS, and JavaScript (ES6 Modules) without build tools.  
- **Hosting:** Statically hosted via GitHub Pages.  
- **Database & Backend:** Powered by Firebase as Backend-as-a-Service (BaaS).  
  - **Firebase Realtime Database:** For real-time data synchronization.  
  - **Firebase Authentication:** For user authentication (Login/Logout).  
- **Device Layer:** ESP8266 devices act as call units in each room, sending data to Firebase.  

## Data Structure (Firebase Realtime Database)

- `alerts_active/{roomId}/{alertId}`: Stores active call objects.  
  - `type`: `"medical"` | `"infusion"` | `"nonmedical"`  
  - `status`: `"Active"` | `"Handled"`  
  - `createdAt`: Timestamp (milliseconds) when the call was created.  
  - `handledAt`: Timestamp (milliseconds) when the call was handled.  
  - `message`: Optional additional message.  

- `alerts_history/{roomId}/{eventId}`: Archive of completed/handled calls. Structure is the same as `alerts_active`.  

## Quick Setup

### 1. Clone Repository
```bash
git clone https://github.com/YOUR_USERNAME/SMARTNURSECALL-YOUR-REPO.git
cd SMARTNURSECALL-YOUR-REPO
```

### 2. Setup Firebase Project
- Open [Firebase Console](https://console.firebase.google.com/).  
- Create a new project (e.g., "smart-nursecall").  
- Enable **Realtime Database** and **Authentication**.  
- In Authentication, enable **Email/Password** sign-in method.  
- Retrieve your project configuration (apiKey, authDomain, databaseURL, etc.) from Project Settings.  
- Create a dedicated user account for ESP8266 devices (e.g., `device@gmail.com`).  

### 3. Configure Web Application
- Open `app.js`, `index.html`, and `dashboard.html`.  
- Replace the `firebaseConfig` variable values with your Firebase project configuration.  

### 4. Configure ESP8266 Device
- Open the ESP8266 code file (`.ino`).  
- Replace `FIREBASE_API_KEY` and `FIREBASE_DATABASE_URL` with your Firebase project configuration.  
- Replace `USER_EMAIL` and `USER_PASSWORD` with the dedicated device account credentials created in step 2.  
- Set a unique `ROOM_ID` for each ESP8266 device (e.g., "001", "002", etc.).  
- Upload the code to the ESP8266 device.  

### 5. Run Locally
- Use the Live Server extension in Visual Studio Code, or  
- Open `index.html` directly in your browser.  

### 6. Deploy to GitHub Pages
- Push all changes to your GitHub repository.  
- Go to your repository, then navigate to **Settings > Pages**.  
- Under "Build and deployment," select **Deploy from a branch**.  
- Choose the `main` (or `master`) branch and folder `/ (root)`.  
- Click **Save**. Your site will be available at:  
  `https://YOUR_USERNAME.github.io/SMARTSNURSECALL-YOUR-REPO`
