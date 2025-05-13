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
- **Events Manager**


Component Overview
------------------

1. User Manager
~~~~~~~~~~~~~~~~
Handles user-related functionalities such as: 
- **Log In/Log Out**: Authenticate users securely.
- **Delete Account**: Permanently remove a user's data.
- **Edit details**: Edit profile details and preferences.

2. Account Manager
~~~~~~~~~~~~~~~~~~~
Responsible for account creation and management:
- **Create Account**: Register new users.
- **Log In/Log Out**: Authenticate user sessions.
- **Delete Account**: Remove user accounts from the system.

3. Matchmaking Manager
~~~~~~~~~~~~~~~~~~~~~~~
Handles the core matchmaking functionality:
- **Generate Matches**: Find compatible users based on preferences.
- **Accept Match**: Users can accept suggested matches.
- **Save Match History**: Keep a record of past matches.

4. Notification Manager
~~~~~~~~~~~~~~~~~~~~~~~~
Manages notifications across the platform:
- **Enable/Disable Notifications**: Allow users to control notifications.
- **Customize Notification Preferences**: Configure notification settings.
- **Send Match Notification**: Notify users of new matches.
- **Send Event Notification**: Notify users about event updates.
- **Send Message Notification**: Alert users about new messages.

5. Messaging Manager
~~~~~~~~~~~~~~~~~~~~~
Manages user interactions via chat:
- **Send Message**: Allow users to communicate.
- **Receive Message**: Retrieve incoming messages.
- **Delete Message**: Remove messages.
- **View Messages**: Display conversation history.
- **Create Group Chat**: Enable multi-user conversations.
- **Edit Group Chat**: Modify group chat settings.
- **Send Media Message**: Allow sharing images, videos, and other files.
- **Write Message**: Draft and send messages.

6. Events Manager
~~~~~~~~~~~~~~~~~~
Manages fitness-related events:
- **Create Event**: Users can set up new events.
- **Edit Event Details**: Modify event information.
- **Delete Event**: Remove an event.
- **View Event Details**: Display event descriptions.

These managers interact with the **database backend**, ensuring authentication, data storage, and real-time updates. The specific database implementation details are covered in :doc:`implementation`.

System Flow
-----------

The architecture follows a structured flow where different managers handle specific functionalities and interact with the Firebase Database for authentication, data storage, and real-time updates.


1. **User Interaction** → Users interact with the UI to perform actions (e.g., login, match, message). 
2. **Manager Processing** → The relevant manager (e.g., User Manager, Matchmaking Manager) processes the request. 
3. **Database Communication** → The Firebase Database handles authentication, data retrieval, and updates. 
4. **UI Update** → The app dynamically updates the interface based on the retrieved data. 

For a more detailed breakdown of the implementation, refer to :doc:`implementation`.