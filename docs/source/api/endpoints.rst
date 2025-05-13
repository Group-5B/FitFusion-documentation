=========================
API Endpoints Overview
=========================

Overview
========
The Matchmaking App interacts with Firebase services through Firestore queries, Firebase Authentication requests, and Firebase Storage paths. This document outlines the key endpoints and data paths used in the implementation.  

Authentication Endpoints
=========================
- **User Registration:**  
  - Endpoint: `FirebaseAuth.createUserWithEmailAndPassword(email, password)`  
  - Purpose: Creates a new user account.  
  - Error Codes: `auth/invalid-email`, `auth/weak-password`, `auth/email-already-in-use`

- **Login:**  
  - Endpoint: `FirebaseAuth.signInWithEmailAndPassword(email, password)`  
  - Purpose: Authenticates the user and establishes a session.  
  - Error Codes: `auth/user-not-found`, `auth/wrong-password`

- **Logout:**  
  - Endpoint: `FirebaseAuth.signOut()`  
  - Purpose: Ends the current session.  

- **Account Deletion:**  
  - Endpoint: `FirebaseAuth.currentUser.delete()`  
  - Purpose: Deletes the user account and triggers data removal from Firestore and Storage.  

Firestore Data Endpoints
========================
- **User Profiles:**  
  - Path: `users/{userId}`  
  - Methods: `GET`, `PUT`, `PATCH`  
  - Example Document Structure:  

    ```json
    {
      "name": "John Doe",
      "email": "john.doe@example.com",
      "location": { "lat": 40.7128, "lng": -74.0060 },
      "preferences": {
        "level": "Intermediate",
        "availability": "Afternoon",
        "gender": "No preference",
        "activities": ["Gym", "Running"]
      }
    }
    ```

- **Matchmaking:**  
  - Path: `matches/{userId}/{matchId}`  
  - Methods: `GET`, `POST`, `DELETE`  
  - Data Structure:  

    ```json
    {
      "matchId": "match123",
      "status": "pending",
      "created_at": "2025-05-12T10:00:00Z"
    }
    ```

- **Chat Messages:**  
  - Path: `chats/{chatId}/messages/{messageId}`  
  - Methods: `GET`, `POST`, `DELETE`  
  - Example Document Structure:  

    ```json
    {
      "senderId": "user123",
      "timestamp": "2025-05-12T12:30:00Z",
      "message": "Hello!",
      "mediaUrl": null
    }
    ```

- **Events:**  
  - Path: `events/{eventId}`  
  - Methods: `GET`, `POST`, `DELETE`  
  - Data Structure:  

    ```json
    {
      "title": "5K Run",
      "date": "2025-06-15T09:00:00Z",
      "location": { "lat": 40.7128, "lng": -74.0060 },
      "participants": ["user123", "user456"]
    }
    ```

Storage Endpoints
=================
- **Profile Pictures:**  
  - Path: `profile_pictures/{userId}.jpg`  
  - Methods: `PUT`, `GET`, `DELETE`

- **Chat Media:**  
  - Path: `chat_media/{chatId}/{messageId}.jpg`  
  - Methods: `PUT`, `GET`, `DELETE`

Notification Endpoints
======================
- **Push Notifications:**  
  - Endpoint: `https://fcm.googleapis.com/fcm/send`  
  - Methods: `POST`  
  - Payload Example:  

    ```json
    {
      "to": "device_token",
      "notification": {
        "title": "New Match!",
        "body": "You have a new match. Check it out!"
      }
    }
    ```

Location Endpoints
==================
- **Update Location:**  
  - Path: `users/{userId}/location`  
  - Methods: `PATCH`  
  - Data Structure:  

    ```json
    {
      "lat": 40.7128,
      "lng": -74.0060
    }
    ```
