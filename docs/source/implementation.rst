Implementation
==============

Overview
========
The Matchmaking App is developed using **Flutter** for cross-platform compatibility and **Firebase** for backend services, including authentication, Firestore, and storage. The app is designed for Web, iOS, and Android, with push notifications managed via Firebase Cloud Messaging and location services via the Geolocator package.  

Backend Structure
=================
- **Firebase Authentication:**  
  - Email and password-based authentication.  
  - Error handling for invalid email formats and weak passwords.  
  - Persistent session management and user state monitoring.  

- **Firestore Database Structure:**  
  - `users` collection: Stores profile data and preferences.  
  - `matches` collection: Tracks matchmaking connections.  
  - `chats` collection: Handles one-to-one and group chat data.  
  - `events` collection: Manages user-created events.  

- **Firebase Storage:**  
  - Stores user profile pictures and media sent in chats.  
  - Implements access control using authentication tokens.  

Registration and Authentication
===============================
- **User Registration:**  
  - Firebase Authentication handles email verification and password encryption.  
  - Validation functions for email domain and password strength implemented in `auth_service.dart`.

- **Login/Logout:**  
  - Login logic checks credentials against Firebase Authentication.  
  - Logout clears user session and navigates to the login screen.

Profile Management
==================
- **Edit Profile:**  
  - User data is fetched from Firestore and displayed using `StreamBuilder`.  
  - Updates are written back to the user's document in the `users` collection.  

- **Profile Picture Upload:**  
  - Image selection uses the `image_picker` package.  
  - Firebase Storage stores images under `profile_pictures/{userId}.jpg`.  
  - Profile images are retrieved with download URLs.

Preferences and Location
========================
- **Preferences Management:**  
  - User preferences are stored in the `preferences` subcollection.  
  - Matching logic retrieves users based on overlapping preferences using Firestore queries.  

- **Location Services:**  
  - Geolocator is used to fetch the current location and update the user's `location` field in Firestore.  
  - Distance calculations are performed using the Haversine formula.

Matchmaking Logic
=================
- **Initial Matchmaking:**  
  - A query is generated based on the current user's preferences and location radius.  
  - Results are displayed as a list of user cards in the `MatchmakingPage`.

- **Preference Updates:**  
  - Updates to preferences trigger new queries to Firestore.  
  - The `getMatchingUsers` function fetches updated matches and listens to changes using `Stream<QuerySnapshot>`.

- **Request Management:**  
  - Match requests are stored in the `matches` collection as subdocuments.  
  - A `request_status` field tracks the state (`pending`, `accepted`, `rejected`).  

Chat Implementation
===================
- **Chat Initialization:**  
  - Upon successful matchmaking, chat rooms are created under `chats/{chatId}`.  
  - Group chat creation involves adding multiple user IDs to the `participants` field.  

- **Real-Time Messaging:**  
  - Chat data is streamed using Firestore listeners.  
  - Media messages are uploaded to Firebase Storage, with download URLs stored in Firestore.

Settings and Notifications
==========================
- **User Settings:**  
  - Font size, dark mode, and notification preferences are stored as fields in the user's Firestore document.  

- **Push Notifications:**  
  - Firebase Cloud Messaging sends notifications for new chat messages and event updates.  
  - Device tokens are managed in Firestore under `users/{userId}/tokens`.

Events Implementation
=====================
- **Event Creation and Search:**  
  - Events are stored in the `events` collection with relevant metadata (activity type, location, date).  
  - Search functionality queries based on activity and proximity.

Account Management
==================
- **Reset Matches:**  
  - Match data is cleared by deleting all `matches` subdocuments for the user.  

- **Account Deletion:**  
  - User data is deleted from Authentication, Firestore, and Storage using batch operations.  

Dependencies
============
- **Firebase:** Authentication, Firestore, Storage, Cloud Messaging.  
- **Geolocator:** Location services and distance calculations.  
- **Image Picker:** Profile picture selection.  
- **Provider:** State management for user data and app settings.  
- **Flutter Material:** UI implementation.  
