Implementation
==============

Overview
--------
- The Matchmaking App is developed using **Flutter** for cross-platform compatibility.  
- Backend services are managed using **Firebase**, including Authentication, Firestore, and Storage.  
- The app supports Web, iOS, and Android, with notifications handled through Firebase Cloud Messaging.  
- Location services are provided by the Geolocator package.  

Backend Structure
-----------------
- **Firebase Authentication:**  
  - Implements email and password-based authentication.  
  - Handles error cases for invalid email formats and weak passwords.  
  - Manages persistent session states and user monitoring.  

- **Firestore Database Structure:**  
  - `users` collection: Stores profile data and preferences.  
  - `matches` collection: Tracks matchmaking connections.  
  - `chats` collection: Manages one-to-one and group chat data.  
  - `events` collection: Manages user-created events.  

- **Firebase Storage:**  
  - Stores user profile pictures and chat media.  
  - Access control is managed through authentication tokens.  

Registration and Authentication
-------------------------------
- User registration is handled by Firebase Authentication with email verification and password encryption.  
- Validation functions are implemented for email domain and password strength.  
- Login logic checks credentials against Firebase Authentication and establishes user sessions.  
- Logout functionality clears user session data and redirects to the login screen.  

Profile Management
------------------
- User profiles are fetched and displayed using `StreamBuilder` from Firestore.  
- Profile updates are written to the `users` collection under specific user IDs.  
- Image selection for profile pictures is managed using the `image_picker` package.  
- Images are stored under `profile_pictures/{userId}.jpg` in Firebase Storage, with download URLs for access.  

Preferences and Location
------------------------
- User preferences are managed under the `preferences` subcollection within each user document.  
- Matchmaking logic compares preferences using Firestore queries.  
- Geolocator fetches the user’s location and updates the `location` field in Firestore.  
- Distance calculations use the Haversine formula to determine proximity.  

Matchmaking Logic
-----------------
- Initial matchmaking retrieves user profiles based on preferences and location radius.  
- The `getMatchingUsers` function listens for Firestore updates using `Stream<QuerySnapshot>`.  
- Preference updates trigger new queries, adjusting the pool of potential matches.  
- Match requests are stored as subdocuments in the `matches` collection with `request_status` fields (`pending`, `accepted`, `rejected`).  

Chat Implementation
-------------------
- Chat rooms are created as new documents in the `chats` collection, identified by unique chat IDs.  
- Group chats include multiple user IDs in the `participants` field.  
- Real-time messaging is enabled through Firestore listeners on the `messages` subcollection.  
- Media messages are uploaded to Firebase Storage, with download URLs saved in the chat document.  

Settings and Notifications
--------------------------
- User settings for font size, dark mode, and notification preferences are stored as fields in the user’s Firestore document.  
- Push notifications are managed using Firebase Cloud Messaging, with device tokens stored in Firestore under `users/{userId}/tokens`.  

Events Implementation
---------------------
- Events are stored in the `events` collection, containing metadata such as activity type, date, and location.  
- Search functionality queries events based on activity type and user location proximity.  

Account Management
------------------
- Match resets are executed by deleting all `matches` subdocuments under the user’s document.  
- Account deletion removes user data from Authentication, Firestore, and Storage using batch operations.  

Dependencies
------------
- **Firebase:** Authentication, Firestore, Storage, Cloud Messaging.  
- **Geolocator:** Handles location services and distance calculations.  
- **Image Picker:** Manages profile picture selection.  
- **Provider:** Manages state for user data and app settings.  
- **Flutter Material:** Implements the UI using Material Design components.  
