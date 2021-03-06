# Casting Agency- Udacity Full stack project

[Link towards API](https://casting-agency-jyrj.herokuapp.com/)

### Motivation for this project

This project is my capstone project for Udacity's Fullstack Nanodegree program. The motivation for the casting agency backend has been provided by Udacity. This application will serve as a backend for a company that is responsible for creating movies and managing and assigning actors to those movies.
Authorized users can interact with the API to view, add, update, delete Movies and Actors details. (RBAC enabled)



## Getting Started

### Installing Dependencies

#### Python 3.7

Follow instructions to install the latest version of python for your platform in the [python docs](https://docs.python.org/3/using/unix.html#getting-and-installing-the-latest-version-of-python)

#### Virtual Enviornment

I recommend working within a virtual environment whenever using Python for projects. This keeps your dependencies for each project separate and organaized. Instructions for setting up a virual enviornment for your platform can be found in the [python docs](https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/)

Another one for easiness is Anaconda environement. Create Python 3.7 conda environment for this project. I have used and tested conda  environment.

#### PIP Dependencies

Once you have your virtual environment setup and running, install dependencies by naviging to the `/backend` directory and running:

```bash
pip install -r requirements.txt
```

This will install all of the required packages we selected within the `requirements.txt` file.


### Endpoints

#### GET /movies

- General:

  - Returns all the movies.
  - Roles authorized : Casting Assistant,Casting Director,Executive Producer.

- Sample: `curl http://127.0.0.1:5000/movies`

```json
{
  "movies": [
    {
      "id": 1,
      "release_date": "Mon, 06 May 2019 00:00:00 GMT",
      "title": "Terminator Dark Fate"
    },
    {
      "id": 2,
      "release_date": "Tue, 06 May 2003 00:00:00 GMT",
      "title": "Terminator Rise of the machines"
    }
  ],
  "success": true
}
```

#### GET /movies/\<int:id\>

- General:

  - Route for getting a specific movie.
  - Roles authorized : Casting Assistant,Casting Director,Executive Producer.

- Sample: `curl http://127.0.0.1:5000/movies/1`

```json
{
  "movie": {
    "id": 1,
    "release_date": "Mon, 06 May 2019 00:00:00 GMT",
    "title": "Terminator Dark Fate"
  },
  "success": true
}
```

#### POST /movies

- General:

  - Creates a new movie based on a payload.
  - Roles authorized : Executive Producer.

- Sample: `curl http://127.0.0.1:5000/movies -X POST -H "Content-Type: application/json" -d '{ "title": "Natasha romanov", "release_date": "2020-05-06" }'`

```json
{
  "movie": {
    "id": 3,
    "release_date": "Wed, 06 May 2020 00:00:00 GMT",
    "title": "Wolf of Wall Street"
  },
  "success": true
}
```

#### PATCH /movies/\<int:id\>

- General:

  - Patches a movie based on a payload.
  - Roles authorized : Casting Director, Executive Producer.

- Sample: `curl http://127.0.0.1:5000/movies/3 -X POST -H "Content-Type: application/json" -d '{ "title": "Natasha romanov patched", "release_date": "2020-05-06" }'`

```json
{
  "movie": {
    "id": 3,
    "release_date": "Wed, 06 May 2020 00:00:00 GMT",
    "title": "Natasha romanov patched"
  },
  "success": true
}
```

#### DELETE /movies/\<int:id\>

- General:

  - Deletes a movies by id form the url parameter.
  - Roles authorized : Executive Producer.

- Sample: `curl http://127.0.0.1:5000/movies/3 -X DELETE`

```json
{
  "message": "movie id 3, titled Spiderman was deleted",
  "success": true
}
```

#### GET /actors

- General:

  - Returns all the actors.
  - Roles authorized : Casting Assistant,Casting Director,Executive Producer.

- Sample: `curl http://127.0.0.1:5000/actors`

```json
{
  "actors": [
    {
      "age": 54,
      "gender": "male",
      "id": 1,
      "name": "Leondardo DiCaprio"
    },
    {
      "age": 50,
      "gender": "male",
      "id": 2,
      "name": "Bruce Wills"
    }
  ],
  "success": true
}
```

#### GET /actors/\<int:id\>

- General:

  - Route for getting a specific actor.
  - Roles authorized : Casting Assistant,Casting Director,Executive Producer.

- Sample: `curl http://127.0.0.1:5000/actors/1`

```json
{
  "actor": {
    "age": 40,
    "gender": "male",
    "id": 1,
    "name": "Will Smith"
  },
  "success": true
}
```

#### POST /actors

- General:

  - Creates a new actor based on a payload.
  - Roles authorized : Casting Director,Executive Producer.

- Sample: `curl http://127.0.0.1:5000/actors -X POST -H "Content-Type: application/json" -d '{ "name": "Mary", "age": 22, "gender": "female" }'`

```json
{
  "actor": {
    "age": 22,
    "gender": "female",
    "id": 3,
    "name": "Mary"
  },
  "success": true
}
```

#### PATCH /actors/\<int:id\>

- General:

  - Patches an actor based on a payload.
  - Roles authorized : Casting Director, Executive Producer.

- Sample: `curl http://127.0.0.1:5000/actors/3 -X POST -H "Content-Type: application/json" -d '{ "name": "John", "age": 22, "gender": "female" }'`

```json
{
  "actor": {
    "age": 22,
    "gender": "female",
    "id": 3,
    "name": "John"
  },
  "success": true
}
```

#### DELETE /actors/<int:id\>

- General:

  - Deletes an actor by id form the url parameter.
  - Roles authorized : Casting Director,Executive Producer.

- Sample: `curl http://127.0.0.1:5000/actors/3 -X DELETE`

```json
{
  "message": "actor id 3, named John was deleted",
  "success": true
}
```

## RBAC - Role Based Access Control

Authentication setup:

The model is having 3 roles
  - Casting assistant: View data from both Actors and Movies models using GET.
  - Casting DIrector: Permissions of assistant with, update actors and movies, add or delete actor.
  - Executive Producer: Permissions of Director with, add/ delete movies.

For the purpose of assesment from Udacity reviewer, I'm providing corresponding Role's JWT which could be used for evaluation purpose. The same could be found in the file jwt_values.py

Successfully tested with Postman. JWT Tokens has set to an expiration of 24 hours.



## Database Setup

The project uses Postgresql as its database, you would need to create one locally and reflect it in setup.sh.
To update the database and seed run the following :

```bash
python manage.py db upgrade
python manage.py seed
```

- you may need to change the database url in setup.sh after which you can run

[IMP]: Please check the environment variables in [setup.sh](setup.sh) before proceeding to run the application.

```bash
source ./setup.sh
```

Start server by running

```bash
python app.py
```
The above will work, well-configured for Heroku deployment.

Below won't work (some small packaging issues with dependencies throw error showing cyclic import exception. Or we must use the same directory for all python files, which I don't prefer)

```bash
flask run
```

##### Key Dependencies

- [Flask](http://flask.pocoo.org/) is a lightweight backend microservices framework. Flask is required to handle requests and responses.

- [SQLAlchemy](https://www.sqlalchemy.org/) is the Python SQL toolkit and ORM we'll use handle the lightweight sqlite database. You'll primarily work in app.py and can reference models.py.

- [Flask-CORS](https://flask-cors.readthedocs.io/en/latest/#) is the extension we'll use to handle cross origin requests from our frontend server.

- [Pycodestyle](https://pypi.org/project/pycodestyle/) - pycodestyle is a tool to check your Python code against some of the style conventions in PEP 8.

## Testing

Replace the jwt tokens in test_app.py with the ones generated on the website.

For testing locally, we need to reset database.
To reset database, run

```
python manage.py db downgrade
python manage.py db upgrade
python manage.py seed
```

### Error Handling

- 401 errors due to RBAC are returned as

```json
{
  "code": "unauthorized",
  "description": "Permission not found."
}
```

Other Errors are returned in the following json format:

```json
{
  "success": "False",
  "error": 422,
  "message": "Unprocessable entity"
}
```

The error codes currently returned are:

- 400 – bad request
- 401 – unauthorized
- 404 – resource not found
- 422 – unprocessable
- 500 – internal server error

### Testing

- For testing the endpoints and RBAC, use test_app.py

```
python test_app.py
```
