# KANTO MAP

## Database Schema Design

## API Documentation

## USER AUTHENTICATION/AUTHORIZATION

### All endpoints that require authentication

All endpoints that require a current user to be logged in.

* Request: endpoints that require authentication
* Error Response: Require authentication
  * Status Code: 401
  * Headers:
    * Content-Type: application/json
  * Body:

    ```json
    {
      "message": "Authentication required",
      "statusCode": 401
    }
    ```

### All endpoints that require proper authorization

All endpoints that require authentication and the current trainer does not have the
correct role(s) or permission(s).

* Request: endpoints that require proper authorization
* Error Response: Require proper authorization
  * Status Code: 403
  * Headers:
    * Content-Type: application/json
  * Body:

    ```json
    {
      "message": "Forbidden",
      "statusCode": 403
    }
    ```

### Get the Current Trainer

Returns the information about the current trainer that is logged in.

* Require Authentication: true
* Request
  * Method: GET
  * URL: /trainers/me
  * Body: none

* Successful Response when there is a logged in trainer
  * Status Code: 200
  * Headers:
    * Content-Type: application/json
  * Body:

    ```json
    {
      "trainer": {
        "id": 1,
        "firstName": "Ash",
        "lastName": "Ketchum",
        "email": "ash.ketchum@gmail.com",
        "username": "foreveryoung",
        "town": {},
        "createdOn": "CURRENT_TIMESTAMP",
        "lastUpdated": "CURRENT_TIMESTAMP"
        }
    }
    ```

* Successful Response when there is no logged in trainer
  * Status Code: 200
  * Headers:
    * Content-Type: application/json
  * Body:

    ```json
    {
      "trainer": null
    }
    ```

### Log In a Trainer

Logs in a current trainer with valid credentials and returns the current trainer's
information.

* Require Authentication: false
* Request
  * Method: POST
  * URL: /trainer/login
  * Headers:
    * Content-Type: application/json
  * Body:

    ```json
    {
      "email": "ash.ketchum@gmail.com",
      "password": "ilovepikachu"
    }
    ```

* Successful Response
  * Status Code: 200
  * Headers:
    * Content-Type: application/json
  * Body:

    ```json
    {
        "trainer": {
        "id": 1,
        "firstName": "Ash",
        "lastName": "Ketchum",
        "email": "ash.ketchum@gmail.com",
        "username": "foreveryoung",
        "town": {},
        "createdOn": "CURRENT_TIMESTAMP",
        "lastUpdated": "CURRENT_TIMESTAMP"
        }
    }
    ```

* Error Response: Invalid credentials
  * Status Code: 401
  * Headers:
    * Content-Type: application/json
  * Body:

    ```json
    {
      "message": "Invalid credentials",
      "statusCode": 401
    }
    ```

* Error response: Body validation errors
  * Status Code: 400
  * Headers:
    * Content-Type: application/json
  * Body:

    ```json
    {
      "message": "Validation error",
      "statusCode": 400,
      "errors": [
        "Email is required",
        "Password is required"
      ]
    }
    ```

### Sign Up a Trainer

Creates a new trainer, logs them in as the current trainer, and returns the current
trainer's information.

* Require Authentication: false
* Request
  * Method: POST
  * URL: /trainers/login
  * Headers:
    * Content-Type: application/json
  * Body:

    ```json
    {
      "firstName": "Gary",
      "lastName": "Oak",
      "email": "gary.oak@gmail.com",
      "password": "ilovepikachuto",
      "username": "foreveroak"
    }
    ```

* Successful Response
  * Status Code: 200
  * Headers:
    * Content-Type: application/json
  * Body:

    ```json
    {
      "user": {
      "firstName": "Gary",
      "lastName": "Oak",
      "email": "gary.oak@gmail.com",
      "password": "ilovepikachuto",
      "username": "foreveroak"
      }
    }
    ```

* Error response: User already exists with the specified email
  * Status Code: 403
  * Headers:
    * Content-Type: application/json
  * Body:

    ```json
    {
      "message": "Trainer already exists",
      "statusCode": 403,
      "errors": [
        "Trainer with that email already exists"
      ]
    }
    ```

* Error response: Body validation errors
  * Status Code: 400
  * Headers:
    * Content-Type: application/json
  * Body:

    ```json
    {
      "message": "Validation error",
      "statusCode": 400,
      "errors": [
        "Invalid email",
        "First Name is required",
        "Last Name is required"
      ]
    }
    ```

## TRAINERS

### Get all Trainers

### Get all Badges of a Trainer specified by id

## POKEMON

### Get all Pokemon

### Get all starter Pokemon

### Get Pokemon by Type

### Get all Pokemon of a certain Trainer

### Get details of a Pokemon by ID

### Create a Pokemon

### Add an Image to a Pokemon based on the pokemon's id

### Edit a Pokemon

### Delete a Pokemon

## GYMS

### Get All GYMS

### Get Badge of a specific GYM by id

### Get GYM Leader of a specific GYM by id

### Create a new GYM

### Edit a GYM specified by id

### Delete a GYM specified by id

## GYM LEADERS

### Get ALL Gym Leaders

### GET Pokemon of a specific GYM Leader by id

### Create a new GYM Leader

- requires a town

### Add an Image to a GYM Leader based on specific id

### Edit a GYM Leader specified by its id

### DELETE a GYM Leader specified by its id

## TOWNS

### GET All Towns

### GET GYM in specified town by id

### Edit a GYM specified by its id

### DELETE a Gym specified by its id

## BADGES

### GET all Badges

### GET all Trainers/GYM Leaders holding specified Badge

## IMAGES

### DELETE Trainer Image

### EDIT Trainer Image

### DELETE Pokemon Image

### Edit Pokemon Image

### DELETE GYM Leader Image

### Edit GYM Leader Image

## Query

### Add Query Filters to Get All Pokemon

Return events filtered by query parameters.

* Require Authentication: false
* Request
  * Method: GET
  * URL: /Events?page=0&size=20
  * Query Parameters
    * page: integer, minimum: 0, maximum: 10, default: 0
    * size: integer, minimum: 0, maximum: 20, default: 20
    * name: string, optional
    * type: string, optional
    * startDate: string, optional
  * Body: none

* Successful Response
  * Status Code: 200
  * Headers:
    * Content-Type: application/json
  * Body:

    ```json
    {
      "Events": [
        {
          "id": 1,
          "groupId": 1,
          "venueId": null,
          "name": "Tennis Group First Meet and Greet",
          "type": "Online",
          "startDate": "2021-11-19 20:00:00",
          "endDate": "2021-11-19 22:00:00",
          "numAttending": 8,
          "previewImage": "image url",
          "Group": {
            "id": 1,
            "name": "Evening Tennis on the Water",
            "city": "New York",
            "state": "NY"
          },
          "Venue": null,
        },
        {
          "id": 1,
          "groupId": 1,
          "venueId": 1,
          "name": "Tennis Singles",
          "type": "In Person",
          "startDate": "2021-11-20 20:00:00",
          "endDate": "2021-11-19 22:00:00",
          "numAttending": 4,
          "previewImage": "image url",
          "Group": {
            "id": 1,
            "name": "Evening Tennis on the Water",
            "city": "New York",
            "state": "NY"
          },
          "Venue": {
            "id": 1,
            "city": "New York",
            "state": "NY",
          },
        },
      ]
    }
    ```

* Error Response: Query parameter validation errors
  * Status Code: 400
  * Headers:
    * Content-Type: application/json
  * Body:

    ```json
    {
      "message": "Validation Error",
      "statusCode": 400,
      "errors": [
        "Page must be greater than or equal to 0",
        "Size must be greater than or equal to 0",
        "Name must be a string",
        "Type must be 'Online' or 'In Person'",
        "Start date must be a valid datetime",
      ]
    }
    ```


how do I layout 1 badge being won by multiple trainers?

and trainers having multiple badges?
