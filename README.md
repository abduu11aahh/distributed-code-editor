### Tools and Technologies used:
This is a web application and uses the following technologies for different coding components:
•	Client Side Code - React (A Javascript Framework).
•	Server Side Code – NodeJS and Express
•	Socket.io Library was used in both client and server side. This library is the core of our application and enables the synchronization of code that is visible to all users. It sends messages to all other users when any of the user makes change in editor. 

### Working:

Our app has two pages:
•	Home Page
•	Editor Page
From our home page we have two options. We can create a new room or join an already created room using the room id. For option 2, the user has to type in the room id in a text field and then submit the form. If the room id exists, the user will be connected to that room.  Only the users that belong to a particular room will be able to view and make changes to the editor.
Editor page is where the user will write code in the editor. The same editor screen will be visible to all users in the room. The user can leave the room by clicking a leave button.

### Architecture:

Our app follows a client server architecture. There are multiple clients that connect with a single server. Different clients can connect and send messages to each other by joining a room. The server handles connecting users in the same room.
All clients that belong to a particular room are grouped together by the server through their room id. The list of room ids are kept in the server and are handled by the Socket.io library. Multiple rooms are kept isolated from one another in a way that no client from different rooms can send its changes to another client in some other room.
When a client creates a room with a unique id, the server will add that room’s id to the list of rooms and send the editor page to the client. When another client wants to joins the room with the same room id, it will send a message to the server with the room id. The server checks if the room id exists. If it does, server will add that user to the room and send the editor page to the client. The server will also send a message to all other clients in the room and inform them that a new client has joined the room.
Whenever a client makes changes to editor, change message is sent to server. The server than broadcasts the change message to all other clients and also sends the snapshot of the editor that has changed along with the request. The other clients receive the change message along with the snapshot and display the received snapshot of editor on their screen.
When a client leaves the room, the server sends a message to all other clients in the same room and informs them that a client has left the room.



### When a new client wants to join a room with id 2:

Step 1: New Client sends room id to server (in our case 2).
Step 2: Server checks for the room id in already created room id’s list.
Step 3: If the room id is found, the server connects the client to that room.
Step 4: The server notifies all clients of the room about the new client.

### Code Synchronization: 


Step 1: A client makes changes to his editor.
Step 2: The client sends a message to server with the snapshot of current state of editor. This snapshot message is sent as soon as the smallest change (typing a letter) is made to the editor.
Step 3: The server sends the editor snapshot to all the clients in the room. This snapshot of editor is now displayed to all users.


### Leaving the room:

Step 1: A client sends an exit message to server.
Step 2: The server disconnects the client from the room and sends a leave notification to all other clients.

