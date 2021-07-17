# RESTFul note app #

RESTFul note application made in Java with Spring allowing user authentication and password reset.

## Back end ##

Only the back end of the app is available. Interaction can be seen on API Endpoint segment.

### Password reset sequence diagram ###

![seq_diagram.png]()

### Password reset class diagram ###

![class_diagram.png]()

### API Endpoint ###

```POST /api/user/password_reset_email```

* Example request

```json
{
"username": "foo@email"
}
```

* Expected response:
  `201 Created`

```json
{
"username": "foo@email",
"token": "abcd1234"
}
```

* Error response with invalid `username`:

  `400 Bad Request`

* Error response with `username` not found:

  `404 Not found`


The password reset token has a timestamp. If a request is done out of the timestamp, the response thrown by the server
will be unauthorized.

`POST /api/user/password`

* Example request

```json
{
"username": "foo@email",
"token": "abcd1234",
"password": "somepassword"
}
```

* Expected response:
  
  `200 OK`

* Expired token o incorrect credentials response:
  
  `401 Unauthorized`

* Token not found response:

  `404 Not Found`

* Malformed headers in request:

  `400 Bad Request`


### Installation ###

```bash
sdk install java 11.0.8.hs-adpt
```

### Environment Variables ###

```bash
export POSTGRES_PASSWORD=root
export APP_DB_PSWD=app
export APP_DB_USER=app
export APP_DB_NAME=app
export APP_AUTH_JWT_SECRET=b898c01c6
```

### Build ###

```bash
./gradlew clean build
```

### Run ###

```bash
./gradlew bootRun
```
