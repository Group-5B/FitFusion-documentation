Architecture
============

This section provides an overview of the FitFusion system architecture, outlining the core components, their responsibilities, and how they interact with the database.

System Overview
---------------

FitFusion follows a modular architecture where different system components handle specific functionalities. The app consists of the following managers:

- **User Manager**
- **Account Manager**
- **Matchmaking Manager**
- **Notification Manager**
- **Messaging Manager**
- **Search Manager**
- **Events Manager**
- **Media Manager**


Component Overview
------------------

### 1. User Manager
Handles user-related functionalities such as:
- **Log In/Log Out**: Authenticate users securely.
- **Delete Account**: Permanently remove a user's data.
- **Reset Password**: Allow users to recover their accounts.
- **Report a Problem**: Enable users to submit issues.
- **Manage Account**: Update user profile and preferences.

### 2. Account Manager
Responsible for account creation and management:
- **Create Account**: Register new users.
- **Log In/Log Out**: Authenticate user sessions.
- **Delete Account**: Remove user accounts from the system.
- **Reset Password**: Assist users in recovering their credentials.
- **Report a Problem**: Allow users to submit issues.
- **Manage Account**: Update personal details.

### 3. Matchmaking Manager
Handles the core matchmaking functionality:
- **Generate Matches**: Find compatible users based on preferences.
- **Accept Match**: Users can accept suggested matches.
- **Save Match History**: Keep a record of past matches.
- **Report Match**: Allow users to report inappropriate matches.

### 4. Notification Manager
Manages notifications across the platform:
- **Enable/Disable Notifications**: Allow users to control notifications.
- **Customize Notification Preferences**: Configure notification settings.
- **Send Match Notification**: Notify users of new matches.
- **Send Event Notification**: Notify users about event updates.
- **Send Message Notification**: Alert users about new messages.
- **Send Promotional Notification**: Inform users about platform updates and promotions.

### 5. Messaging Manager
Manages user interactions via chat:
- **Send Message**: Allow users to communicate.
- **Receive Message**: Retrieve incoming messages.
- **Delete Message**: Remove messages.
- **View Messages**: Display conversation history.
- **Create Group Chat**: Enable multi-user conversations.
- **Edit Group Chat**: Modify group chat settings.
- **Mark Message as Read**: Track message status.
- **Send Media Message**: Allow sharing images, videos, and other files.
- **Write Message**: Draft and send messages.
- **Report Message**: Allow users to flag inappropriate messages.

### 6. Search Manager
Handles user search functionality:
- **Perform Search**: Find users, events, or matches.
- **Delete Search History**: Allow users to remove past searches.
- **Create Search History**: Store recent searches for quick access.

### 7. Events Manager
Manages fitness-related events:
- **Create Event**: Users can set up new events.
- **Edit Event Details**: Modify event information.
- **Delete Event**: Remove an event.
- **View Event Details**: Display event descriptions.
- **Join Event**: Allow users to participate in an event.
- **Leave Event**: Enable users to opt out of an event.

### 8. Media Manager
Handles all media-related operations:
- **Load Media**: Retrieve stored images, videos, and other files.
- **Share Media**: Allow users to send media within the app.
- **Store Media**: Save uploaded files securely.
- **Download Media**: Provide options for users to download content.

These managers interact with the **database backend**, ensuring authentication, data storage, and real-time updates. The specific database implementation details are covered in :doc:`implementation`.

System Flow
-----------

The architecture follows a structured flow where different managers handle specific functionalities and interact with the Firebase Database for authentication, data storage, and real-time updates.

.. image:: images/architecture_diagram.png
   :alt: FitFusion System Architecture
   :align: center
   :width: 80%

The key flow of operations:
1. **User Interaction** → Users interact with the UI to perform actions (e.g., login, match, message).
2. **Manager Processing** → The relevant manager (e.g., User Manager, Matchmaking Manager) processes the request.
3. **Database Communication** → The Firebase Database handles authentication, data retrieval, and updates.
4. **UI Update** → The app dynamically updates the interface based on the retrieved data.

For a more detailed breakdown of the implementation, refer to :doc:`implementation`.