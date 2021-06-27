# mesothelae

A chat program using Flask backend and some sort of html frontend

## Contents of README
- [Organisation of documentation](#organisation-of-documentation)
- [Organisation of project](#organisation-of-project)
- [Terms used in this project](#terms-used-in-this-project)
- [Development timeline](#development-timeline)
- [Planned features for initial release](#planned-features-for-initial-release)
- [Planned future features](#planned-future-features)
- [Data storage](#data-storage)
- [Code architecture](#code-architecture)

## Organisation of documentation

Unlike my previous projects, which had countless documentation files, all of the documentation for developers will be kept in one file. This will hopefully keep the file system neater, avoid me spending hours pasting links to the files everywhere and probably be easier to navigate. Note that *user* documentation should be stored seperately, in a user-friendly format (i.e not markdown).

## Organisation of project

Instead of using subfolders to organise the sections of the program (eg backend frontend etc), which gets messy and makes deployment annoying (why should the backend have to be put in the `/var/www/html` or whatever), the different sections are going to be organised by putting them in different git branches. Currently there are two branches:
- `master` stores the editor documentation and the license
- `prototype` stores an early tester used to gain familiarity with WSGI and probe different options for architecture.

Here are some possible planned branches:
- `main` stores the Flask program and all of the HTML is serves (used if I decide to have Flask serving HTML as well as being a backend)
- `backend` will store the Flask backend (used if backend and frontend are seperated)
- `frontend` will store a HTML frontend (used if backend and frontend are seperated)
- `python-frontend` will store a possible downloadable frontend written in python

## Terms used in this project
- A 'user' is a person who has signed up. A user can also refer to the data structure representing the user
- An 'account' is a username/password combination that users think they own.
- A 'message' is a piece of text that one user has sent into a room.
- A 'room' is a place where users can interact by sending messages. Rooms are created by users. Only those who have joined the room can view messages in it or send messages in it. To join a room, you must be invited by the owner.
- The 'owner' of a room refers to the user who created it.
- A 'member' of a room is a user who has been invited
- A 'page' is a webpage in the frontend that users can navigate to.

## Development timeline

In an effort to develop this project in a timely and organised manner, I've decided to create a development plan and timeline. These dates aren't fixed and can be moved back of forward if required.
- 28 June - 4 July: Decide upon overall architecture. This includes deciding whether Flask will serve HTML or only act as a server, how/where to organise the data, how to organise the code, protocols of communication between server and client and what features will be present in initial deployment.
- 5 July - 12 July: Organise the branches on GitHub and put folders etc in each. Set up testing environment, including WSGI stuff. Start writing documentation on how to set up project on a server. Create a small test server program and use it to test creating and using websockets. Write data storage and retrieval. Create helper functions for finding users, etc.
- 13 July - 20 July: 
- 

During this period, the documentation will also be continuously updated to reflect the latest changes and to change from 'will' to 'is'.

## Planned features for initial release

- People can create an account and thus become a user
- Accounts will have password security, a unique username and a display name
- Users can change their display name and password
- Users can delete their account
- Users can create rooms
- Room owners can configure their rooms - renaming room, deleting room, adding members
- Users can send plain text messages in rooms that they are a member of

## Planned future features

(In no particular order)
- Users can search for rooms
- Users can search for other users and view their profiles
- Users can add a markdown bio to their profile
- Users can send a request to join a room
- Users can now remove themself from rooms
- Users can be kicked from rooms by the owner
- Users can select light-dark theme
- Messages are now sent in markdown format, allowing formatting and code blocks
- Users can select some basic preferences like shortcut to send

## Data storage

The data will be stored in json format, using a custom module for saving and error handling. The data will be broken up into a number of files.

#### Data files

`rooms.json` will hold a list of `Room` data structures
`users.json` will hold a list of `User` data structures
`sessionIds.json` will hold a list of `SessionId` data structures

#### Data structures

###### User

I can't decide whether users should have a unique username or a unique id so I wrote both
- `username` - a unique, unchangable string that the user sets on registering
- `id` - a unique, unchangable integer set automatically on registering.
- `display_name` - The name that the user is shown as to others. Can be changed and is not unique
- `password_hash` - A hash of the user's password. Obviously not unique.

###### SessionId

Fields:
- `username`/`user_id` - this refers to the `User` that the session id is for.
- `value` - a bunch of random letters etc that make up the code. Should be unique.
- `expires` - an integer that signifies the time of expiry of this id. In milliseconds since epoch.

###### Room

Fields:
- `id` - a unique integer id created automatically on creation.
- `name` - the name that is displayed to users. Can be changed and is not unique
- `owner` - the username/id of the user who owns this room
- `members` - a list of usernames/ids of users who are in the room. Is changed every time a user joins or leaves. Should include the username/id of the owner
- `messages` - a list 

###### Message

Fields:
- `sender` - the username/id of the user who sent the message
- `content` - a string that is the content of the message
- `timestamp` - milliseconds since epoch of when the message was sent (added to message list)

## Code architecture

I haven't started writing code yet but I just wanted to prepare a heading.