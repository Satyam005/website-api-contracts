# Users Status

## Users Status object

```
{
  "userId": "String",
  "currentStatus":  {
      "state": "OOO | IDLE | ACTIVE",
      "updatedAt": "TimeStamp",
      "from": "TimeStamp ",
      "until": "TimeStamp",
      "message": "String"
    },
  "futureStatus":  {
      "state": "OOO | IDLE | ACTIVE",
      "updatedAt": "TimeStamp",
      "from": "TimeStamp ",
      "until": "TimeStamp",
      "message": "String"
    },
  "monthlyHours": {
      "committed": "Integer",
      "updatedAt": "TimeStamp"
    }
}
```

**Note:** The futureStatus can only be updated internally. It is used to store future status. and when the right times arrive it updates the current status with the future staus.A user can only send current Status in patch request.

## **Requests**

|                   Route                    |                           Description                           |
| :----------------------------------------: | :-------------------------------------------------------------: |
|      [GET /users/status](#get-users)       |     Returns the Users Status of all the Users in the system     |
|  [GET /users/status/self](#get-usersSelf)  |     Returns the Users Status details of the logged in User      |
|   [GET /users/status/:id](#get-usersid)    |         Returns the User Status data with the given id          |
|  [PATCH /users/status/self](#post-users)   | Creates or Updates a new User Status data of the logged in User |
| [PATCH /users/status/:userId](#post-users) |   Creates or Updates a new User Status data with the given id   |
|   [DELETE /users/self](#patch-usersself)   |   Deletes the User Status data of the User with the given id    |

## **GET /users/status**

Returns the users status of all the users in the system.

- **Params**  
  None
- **Query**  
  state=[OOO | IDLE | ACTIVE]
- **Body**  
  None
- **Headers**  
  Content-Type: application/json
- **Cookie**  
  rds-session: `<JWT>`
- **Success Response:**
  - **Code:** 200
    - **Content:** `{
      message: 'All User Status found successfully.'
      users: [
              {<user_status_object>}
            ]
    }`
- **Error Response:**
  - **Code:** 500
    - **Content:** `{ 'statusCode': 500, 'error': 'Internal Server Error', 'message': 'An internal server error occurred' }`

## **GET /users/status/self**

Returns the Users Status details of the logged in User.

- **Params**  
  None
- **Query**
  None
- **Body**  
  None
- **Headers**  
  Content-Type: application/json
- **Cookie**  
  rds-session: `<JWT>`
- **Success Response:**
  - **Code:** 200
    - **Content:** `{ 'id':'documentId' ,'userId':'userId', data:<user_status_object>,"message": User Status found successfully. }`
- **Error Response:**
  - **Code:** 401
    - **Content:** `{ 'statusCode': 401, 'error': 'Unauthorized', 'message': 'Unauthenticated User' }`
  - **Code:** 404
    - **Content:** `{ 'statusCode': 404, 'error': 'Not Found', 'message': 'User Status couldn't be found.' }`
  - **Code:** 500
    - **Content:** `{ 'statusCode': 500, 'error': 'Internal Server Error', 'message': 'The User Status could not be found as an internal server error occurred.' }`

## **GET /users/status/:userId**

Returns the User Status data with the given User Id.

- **Params**  
  _Required:_ `userId=[string]`
- **Body**  
  None
- **Headers**  
  Content-Type: application/json
- **Cookie**  
  rds-session: `<JWT>`
- **Success Response:**
- **Code:** 200
  - **Content:** `{ 'id':'documentId' ,'userId':'userId', data:<user_status_object>,"message": User Status found successfully. }`
- **Error Response:**
  - **Code:** 401
    - **Content:** `{ 'statusCode': 401, 'error': 'Unauthorized', 'message': 'Unauthenticated User' }`
  - **Code:** 404
    - **Content:** `{ 'statusCode': 404, 'error': 'Not Found', 'message': 'User Status couldn't be found.' }`
  - **Code:** 500
    - **Content:** `{ 'statusCode': 500, 'error': 'Internal Server Error', 'message': 'The User Status could not be found as an internal server error occurred.' }`

## **PATCH /users/status/self**

Creates or Updates a new User Status data of the logged in User.

- **Params**  
  None
- **Query**  
  None
- **Headers**  
  Content-Type: application/json
- **Cookie**  
  rds-session: `<JWT>`
- **Body** `{ <user_status_object> }`
- **Success Response:**
  - **Code:** 201|200
    - **Content:** `{'id':'documentId' ,'userId':'userId','data': <user_object>,"message": "User Status created successfully. | User Status updated successfully. " }`
- **Error Response:**
  - **Code:** 401
    - **Content:** `{ 'statusCode': 401, 'error': 'Unauthorized', 'message': 'Unauthenticated User' }`
  - **Code:** 500
    - **Content:** `{ 'statusCode': 500, 'error': 'Internal Server Error', 'message': 'An internal server error occurred' }`

## **PATCH /users/status/:userId**

Updates data of the User.

- **Params**  
  _Required:_ `userId=[string]`
- **Query**  
  None
- **Headers**  
  Content-Type: application/json
- **Cookie**  
  rds-session: `<JWT>`
- **Body** `{ <user_status_object> }`
- **Success Response:**
  - **Code:** 201|200
    - **Content:** `{'id':'documentId' ,'userId':'userId','data': <user_object>,"message": "User Status created successfully. | User Status updated successfully. " }`
- **Error Response:**
  - **Code:** 401
    - **Content:** `{ 'statusCode': 401, 'error': 'Unauthorized', 'message': 'Unauthenticated User' }`
  - **Code:** 500
    - **Content:** `{ 'statusCode': 500, 'error': 'Internal Server Error', 'message': 'An internal server error occurred' }`

## **DELETE /users/status/:userId**

Deletes the User Status data of the User with the given id.

- **Params**  
  _Required:_ `userId=[string]`
- **Query**  
  None
- **Headers**  
  Content-Type: application/json
- **Cookie**  
  rds-session: `<JWT>`
- **Body**
  None
- **Success Response:**
  - **Code:** 201|200
    - **Content:** `{'id':'documentId' ,'userId':'userId',"message": "User Status deleted successfully." }`
- **Error Response:**
  - **Code:** 401
    - **Content:** `{ 'statusCode': 401, 'error': 'Unauthorized', 'message': 'Unauthenticated User' }`
  - **Code:** 404
    - **Content:** `{ 'statusCode': 404, 'id': null ,'userId':'userId',"message": "User Status to delete not found." }`
  - **Code:** 500
    - **Content:** `{ 'statusCode': 500, 'error': 'Internal Server Error', 'message': 'An internal server error occurred' }`
