Implementation
==============

This section provides an overview of the implementation of the FitFusion app, detailing how each core functionality is realized using Flutter and Firebase.  

System Overview
---------------

The implementation of FitFusion leverages Firebase services for authentication, data storage, and notifications. Flutter is used for UI development across Web, iOS, and Android platforms. The app follows a modular structure with distinct managers handling specific functionalities:  

- **Authentication and Registration**  
- **Profile Management**  
- **Preferences and Location**  
- **Matchmaking**  
- **Chat Management**  
- **Settings and Notifications**  
- **Event Management**  
- **Account Management**  

Component Implementation
------------------------

1. Authentication and Registration
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Handles user authentication, registration, and session management:  
- **Register User**: Creates a new user account using `FirebaseAuth.createUserWithEmailAndPassword`.  
- **Login**: Verifies user credentials and initiates a session using `FirebaseAuth.signInWithEmailAndPassword`.  
- **Logout**: Ends the current session using `FirebaseAuth.signOut()`.  
- **Password Validation**: Ensures passwords meet complexity requirements.  
- **Account Deletion**: Deletes the user account and associated data from Firestore and Storage.  

2. Profile Management
~~~~~~~~~~~~~~~~~~~~~~
Manages user profile data and updates:  
- **Edit Profile**: Allows users to update their information stored in the `users` collection.  
- **Upload Profile Picture**: Uses `image_picker` for image selection and Firebase Storage for uploading.  
- **Retrieve Profile Data**: Fetches profile data using Firestore queries.  
- **Update Preferences**: Updates user preferences in the `preferences` subcollection.  

3. Preferences and Location
~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Handles user preferences and location data:  
- **Set Preferences**: Updates activity, level, availability, and gender preferences.  
- **Update Location**: Uses Geolocator to fetch coordinates and updates the `location` field in Firestore.  
- **Distance Calculation**: Determines proximity between users using the Haversine formula.  

4. Matchmaking
~~~~~~~~~~~~~~~
Implements the core matchmaking logic:  
- **Generate Matches**: Queries potential matches based on preferences and location.  
- **Update Preferences and Radius**: Adjusts the pool of matches by updating the search criteria.  
- **Send Match Request**: Creates a match request in the `matches` collection with status `pending`.  
- **Accept/Reject Request**: Updates the `request_status` field to `accepted` or `rejected`.  
- **Match Reset**: Deletes all match requests for the user.  

5. Chat Management
~~~~~~~~~~~~~~~~~~~
Handles messaging and group chat functionality:  
- **Create Chat Room**: Initializes a chat room document under the `chats` collection.  
- **Send Message**: Sends messages with timestamp and sender ID.  
- **Receive Messages**: Streams incoming messages using Firestore listeners.  
- **Media Sharing**: Uploads media files to Firebase Storage and stores download URLs in Firestore.  
- **Group Chat**: Allows multiple participants to join a single chat room.  
- **Delete Chat**: Removes chat data from Firestore.  

6. Settings and Notifications
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Manages user settings and push notifications:  
- **Update Font Size and Theme**: Stores preferences in Firestore.  
- **Enable/Disable Notifications**: Updates notification settings based on user input.  
- **Send Notifications**: Sends notifications via Firebase Cloud Messaging, targeting specific device tokens.  
- **Receive Notifications**: Handles incoming notifications to display alerts and update the UI.  

7. Event Management
~~~~~~~~~~~~~~~~~~~~
Implements event creation, search, and management:  
- **Create Event**: Allows users to set up fitness-related events in the `events` collection.  
- **Edit Event**: Modifies existing event data.  
- **Search Events**: Queries events based on activity type and location.  
- **Delete Event**: Removes event data from Firestore.  

8. Account Management
~~~~~~~~~~~~~~~~~~~~~~
Handles account-level operations:  
- **Reset Matches**: Clears all match requests and history.  
- **Delete Account**: Executes a batch operation to remove user data from Authentication, Firestore, and Storage.  
- **Sign Out**: Clears user session and redirects to the login screen.  

Data Flow
---------

The data flow across the app follows a structured process:  
1. **User Action** → User performs an action (e.g., update profile, send a message).  
2. **Data Processing** → The relevant manager processes the request and updates Firestore or Storage.  
3. **Data Synchronization** → Firestore listeners update the UI with the latest data in real time.  
4. **Notification Dispatch** → Firebase Cloud Messaging sends alerts based on user actions (e.g., new match, new message).  

Dependencies
------------

The FitFusion app relies on several key dependencies:  
- **Firebase**: Authentication, Firestore, Storage, Cloud Messaging.  
- **Geolocator**: Provides location data for proximity-based matchmaking.  
- **Image Picker**: Handles image selection for profile pictures and media sharing.  
- **Provider**: Manages state and data flow across the app.  
- **Flutter Material**: Implements the user interface using Material Design components.  
