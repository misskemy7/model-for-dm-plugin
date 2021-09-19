# model-for-dm-plugin
These models show descriptions of the format of what you either  post or get.
- **Strings** are characters that are enclosed within codes.
- **Max-length** is the maximum number of characters to be entered
- **Min-length** the the minimum number of characters


 ## Message link Response ; 
 The message link response  creates a link for a particular message. It takes the room and message id’s and converts it to a link.
 
 ```
{
room_id
string
title: Room id
readOnly: true
message_id
string
title: Message id
readOnly: true
link
string($uri)
title: Link
readOnly: true
minLength: 1
}
```

## Room:  
The room has an organization id which is the organization using that room.
 - **Room user ids;**  shows a List of strings of the user id’s of the two users in a  direct message.
- **Bookmarks** show the list of the users that bookmark a particular message.
- **Pinned** shows the list of the users that pinned a particular message
- **the fields on astericks are very important.**

```
org_id*
string
title: Org id
maxLength: 128
minLength: 1
room_user_ids*
[string
maxLength: 128
minLength: 1]
bookmarks*
[string
maxLength: 128
minLength: 1]
pinned*
[string
maxLength: 128
minLength: 1]
created_at
string($date-time)
title: Created at
readOnly: true
default: 2021-09-16T08:29:25.303576Z
}
```

## CREATE ROOM RESPONSE
```
{
room_id
string
title: Room id
readOnly: true
} 
```

## MESSAGE RESPONSE 
It takes a status (read or not), message id and a thread (if it has a thread).

```
{
status
string
title: Status
readOnly: true
minLength: 1
message_id
string
title: Message id
readOnly: true
thread*
boolean
title: Thread
data
Data{
< * >:
string
minLength: 1
}
created_at
string($date-time)
title: Created at
readOnly: true
}
```

## ROOM INFO RESPONSE
 It gives information about a particular room. It has the Id of the room, the organization that owns the room, the id’s of the users of that room and the description of the room (example: this chat is between...)

```
{
_id
string
title: id
readOnly: true
org_id
string
title: Org id
readOnly: true
minLength: 1
room_user_ids*
[string
minLength: 1]
created_at
string($date-time)
title: Created at
readOnly: true
description
string
title: Description
readOnly: true
minLength: 1
}
```

## THREAD 
A thread is like a message within a message. it contains the id of the message, the sender id, the message and media contained in the message.
```
{
message_id*
string
title: Message id
maxLength: 128
minLength: 1
sender_id*
string
title: Sender id
maxLength: 128
minLength: 1
message*
string
title: Message
minLength: 1
media
[
default: List []
string($uri)
minLength: 1]
created_at
string($date-time)
title: Created at
default: 2021-09-16T08:29:25.315456Z
}
```

## MESSAGE 
- **Room id** specifies the room that a message belongs to so that if queries are to be made, it can be referenced. 
- **Message** contains the information that is sent
- **Media field** stores the url for whatever media that is sent.
- **Read field** the default is usually false( that is, it has not been read)
- **Pinned** it is  boolean (true or false)
- **Saved by** it has a saving functionality. it  takes a list of users that saved a particular message.
- **Threads** takes in a message id, sender id, and message. It is  basically a message within a message.

```
{
sender_id*
string
title: Sender id
maxLength: 128
minLength: 1
room_id*
string
title: Room id
maxLength: 128
minLength: 1
message*
string
title: Message
minLength: 1
media
[
default: List []
string($uri)
minLength: 1]
read
boolean
title: Read
default: false
pinned
boolean
title: Pinned
default: false
saved_by
[
default: List []
string
maxLength: 128
minLength: 1]
threads
[
default: List []
Thread{
message_id*
string
title: Message id
maxLength: 128
minLength: 1
sender_id*
string
title: Sender id
maxLength: 128
minLength: 1
message*
string
title: Message
minLength: 1
media
[...]
created_at
string($date-time)
title: Created at
default: 2021-09-16T08:29:25.315456Z
}]
created_at
string($date-time)
title: Created at
default: 2021-09-16T08:29:25.316043Z
}
```


## THREAD RESPONSE
 it is used to get information about a particular thread.
 
 ```
{
status
string
title: Status
readOnly: true
minLength: 1
message_id
string
title: Message id
readOnly: true
thread_id
string
title: Thread id
readOnly: true
thread*
boolean
title: Thread
data
Data{
< * >:
string
minLength: 1
}
created_at
string($date-time)
title: Created at
readOnly: true
}
```
# model-for-dm-plugin
