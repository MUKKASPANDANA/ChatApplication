# Chat Application:

Working Link:https://chatapp-b9c68.web.app/
  - 1. Overview
       - The chat application enables real-time communication between multiple users using WebSockets. It works by establishing a persistent connection between each client           (browser) and the server, allowing messages to be sent and received instantly without page reloads.

  - 2. Flow of the Application
      - Step 1: User Authentication (Choosing a Username)
      - When a user visits the application, they are prompted to enter a unique username.
      - The system checks whether the username is already in use:
         - If available: The user is allowed to proceed to room selection.
         - If not: The user is asked to choose another username.
      - Why?
      - This prevents impersonation and ensures every user in the chat is uniquely identifiable.

   - # Step 2: Room Selection and Management
       - After choosing a username, the user:
          - Selects an existing chat room from the list.
          - Or creates a new chat room.
       - The server keeps track of:
          - Which rooms exist.
          - Which users are currently in each room.
       - When a new room is created, it becomes visible to other users instantly.
       - Why?
       - This feature allows users to form different groups for separate conversations.

   -  # Step 3: Establishing Real-Time Connection
       -  Once a user joins a room, their browser:
          -  Connects to the WebSocket server.
          -  Registers the user in the selected room.
       -  The server maintains a persistent connection:
          -  Any message sent by a user is broadcast to all users in that room.
          -  There’s no need to refresh the page because messages are pushed directly to the browser.
       -  Why?
       -  This ensures instant messaging and eliminates delays common in traditional HTTP requests.
   -  # Step 4: Sending & Receiving Messages
       -  When a user sends a message:
         -  The message is sent to the WebSocket server along with:
             -  Username (who sent it)
             -  Room name
             -  Timestamp
        -  The server broadcasts it to all users in that room.
       -  When a user receives a message:
          -  The chat UI automatically updates with:
              -  Sender’s name
              -  Message content
              -  Time the message was sent
       -  Additional Features:
          -  Auto-scrolling: Always shows the latest message.
          -  Basic formatting: Allows bold, italics, and hyperlinks.

  - # Step 5: Notifications & User Experience
     - When a new message arrives:
        - The chat window scrolls down automatically.
        - If the user is not on the current room tab, they receive a notification.
     - Empty messages or invalid inputs are blocked by validation checks.
     - Why?
     - This improves usability and ensures smooth communication.
   - # Step 6: Handling Disconnects
     - If a user closes the tab or loses connection:
        - The server removes them from the active room.
        - Remaining users see that the user has left.
     - This prevents "ghost users" in rooms.

  - 3. Behind the Scenes (Technical Workflow)
     - 1. User enters a username → Validated by the server.
     - 2. User selects/creates a room → Server stores user in that room.
     - 3. User sends a message → Sent to server → Broadcast to all room members.
     - 4. Users receive messages instantly → UI updates without refresh.
     - 5. User disconnects → Server updates room list & notifies others.
