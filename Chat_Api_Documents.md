# Chat Server API Documentation

## Overview
This document outlines the cloud functions available in the Parse Server application for managing rooms and messages, along with example implementations for Android, iOS, and Flutter.

## Cloud Functions

### 1. `createRoom`

- **Description**: Creates a new room.
- **Parameters**:
  - `name` (String): The name of the room.
  - `createdBy` (String): The user ID of the creator.
  - `users` (Array): An array of user IDs included in the room.
- **Returns**: The newly created room object.

**Example Calls**:

#### Android
```java
ParseCloud.callFunctionInBackground("createRoom", params, new FunctionCallback<ParseObject>() {
    @Override
    public void done(ParseObject room, ParseException e) {
        if (e == null) {
            // room created successfully
        }
    }
});
```

#### iOS
```swift
let params: [String: Any] = ["name": "Room 1", "createdBy": "userId1", "users": ["userId1"]]
PFCloud.callFunction(inBackground: "createRoom", withParameters: params) { (result, error) in
    if error == nil {
        // room created successfully
    }
}
```

#### Flutter
```dart
final params = {
  "name": "Room 1",
  "createdBy": "userId1",
  "users": ["userId1"],
};

final response = await ParseCloud.callFunction('createRoom', params: params);
```

---

### 2. `addUserToRoom`

- **Description**: Adds a user to an existing room.
- **Parameters**:
  - `roomId` (String): The ID of the room.
  - `userId` (String): The ID of the user to be added.
- **Returns**: The updated room object.

**Example Calls**:

#### Android
```java
Map<String, String> params = new HashMap<>();
params.put("roomId", roomId);
params.put("userId", userId);
ParseCloud.callFunctionInBackground("addUserToRoom", params, new FunctionCallback<ParseObject>() {
    @Override
    public void done(ParseObject room, ParseException e) {
        if (e == null) {
            // user added successfully
        }
    }
});
```

#### iOS
```swift
let params: [String: Any] = ["roomId": roomId, "userId": userId]
PFCloud.callFunction(inBackground: "addUserToRoom", withParameters: params) { (result, error) in
    if error == nil {
        // user added successfully
    }
}
```

#### Flutter
```dart
final params = {
  "roomId": roomId,
  "userId": userId,
};

final response = await ParseCloud.callFunction('addUserToRoom', params: params);
```

---

### 3. `fetchChatMessages`

- **Description**: Fetches chat messages from a specific room with pagination.
- **Parameters**:
  - `roomId` (String): The ID of the room.
  - `page` (Number, optional): The page number to fetch (default is 1).
  - `limit` (Number, optional): The number of messages to retrieve per page (default is 50).
- **Returns**: An object containing chat messages, pagination details, and total messages.

**Example Calls**:

#### Android
```java
Map<String, Object> params = new HashMap<>();
params.put("roomId", roomId);
params.put("page", 1);
params.put("limit", 10);
ParseCloud.callFunctionInBackground("fetchChatMessages", params, new FunctionCallback<Object>() {
    @Override
    public void done(Object result, ParseException e) {
        if (e == null) {
            // handle messages
        }
    }
});
```

#### iOS
```swift
let params: [String: Any] = ["roomId": roomId, "page": 1, "limit": 10]
PFCloud.callFunction(inBackground: "fetchChatMessages", withParameters: params) { (result, error) in
    if error == nil {
        // handle messages
    }
}
```

#### Flutter
```dart
final params = {
  "roomId": roomId,
  "page": 1,
  "limit": 10,
};

final response = await ParseCloud.callFunction('fetchChatMessages', params: params);
```

---

### 4. `createPrivateRoom`

- **Description**: Creates a private room between two users.
- **Parameters**:
  - `otherUsername` (String): The username of the other user in the private room.
  - `roomName` (String): The name of the private room.
- **Returns**: The newly created private room object.

**Note**: Requires user authentication.

**Example Calls**:

#### Android
```java
Map<String, String> params = new HashMap<>();
params.put("otherUsername", otherUsername);
params.put("roomName", roomName);
ParseCloud.callFunctionInBackground("createPrivateRoom", params, new FunctionCallback<ParseObject>() {
    @Override
    public void done(ParseObject room, ParseException e) {
        if (e == null) {
            // private room created successfully
        }
    }
});
```

#### iOS
```swift
let params: [String: Any] = ["otherUsername": otherUsername, "roomName": roomName]
PFCloud.callFunction(inBackground: "createPrivateRoom", withParameters: params) { (result, error) in
    if error == nil {
        // private room created successfully
    }
}
```

#### Flutter
```dart
final params = {
  "otherUsername": otherUsername,
  "roomName": roomName,
};

final response = await ParseCloud.callFunction('createPrivateRoom', params: params);
```

---

### 5. `listPrivateRooms`

- **Description**: Lists all private rooms the specified user is part of.
- **Parameters**:
  - `userId` (String): The ID of the user whose private rooms are to be listed.
- **Returns**: An array of private room objects.

**Example Calls**:

#### Android
```java
Map<String, String> params = new HashMap<>();
params.put("userId", userId);
ParseCloud.callFunctionInBackground("listPrivateRooms", params, new FunctionCallback<List<ParseObject>>() {
    @Override
    public void done(List<ParseObject> rooms, ParseException e) {
        if (e == null) {
            // handle rooms
        }
    }
});
```

#### iOS
```swift
let params: [String: Any] = ["userId": userId]
PFCloud.callFunction(inBackground: "listPrivateRooms", withParameters: params) { (result, error) in
    if error == nil {
        // handle rooms
    }
}
```

#### Flutter
```dart
final params = {
  "userId": userId,
};

final response = await ParseCloud.callFunction('listPrivateRooms', params: params);
```

---

### 6. `createPublicRoom`

- **Description**: Creates a public room.
- **Parameters**:
  - `name` (String): The name of the room.
  - `createdBy` (String): The user ID of the creator.
- **Returns**: The newly created public room object.

**Example Calls**:

#### Android
```java
Map<String, String> params = new HashMap<>();
params.put("name", roomName);
params.put("createdBy", createdBy);
ParseCloud.callFunctionInBackground("createPublicRoom", params, new FunctionCallback<ParseObject>() {
    @Override
    public void done(ParseObject room, ParseException e) {
        if (e == null) {
            // public room created successfully
        }
    }
});
```

#### iOS
```swift
let params: [String: Any] = ["name": roomName, "createdBy": createdBy]
PFCloud.callFunction(inBackground: "createPublicRoom", withParameters: params) { (result, error) in
    if error == nil {
        // public room created successfully
    }
}
```

#### Flutter
```dart
final params = {
  "name": roomName,
  "createdBy": createdBy,
};

final response = await ParseCloud.callFunction('createPublicRoom', params: params);
```

---

### 7. `listRooms`

- **Description**: Lists all public rooms with pagination.
- **Parameters**:
  - `page` (Number, optional): The page number to fetch (default is 1).
  - `limit` (Number, optional): The number of rooms to retrieve per page (default is 10).
- **Returns**: An object containing public rooms, pagination details, and total rooms.

**Example Calls**:

#### Android
```java
Map<String, Object> params = new HashMap<>();
params.put("page", 1);
params.put("limit", 10);
ParseCloud.callFunctionInBackground("listRooms", params, new FunctionCallback<Object>() {
    @Override
    public void done(Object result, ParseException e) {
        if (e == null) {
            // handle public rooms
        }
    }
});
```

#### iOS
```swift
let params: [String: Any] = ["page": 1, "limit": 10]
PFCloud.callFunction(inBackground: "listRooms", withParameters: params) { (result, error) in
    if error == nil {
        // handle public rooms
    }
}
```

#### Flutter
```dart
final params = {
  "page": 1,
  "limit": 10,
};

final response = await ParseCloud.callFunction('listRooms', params: params);
```

---
