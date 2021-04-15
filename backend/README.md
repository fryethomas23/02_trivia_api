# Full Stack Trivia API Backend

## Getting Started

### Installing Dependencies

#### Python 3.7

Follow instructions to install the latest version of python for your platform in the [python docs](https://docs.python.org/3/using/unix.html#getting-and-installing-the-latest-version-of-python)

#### Virtual Enviornment

We recommend working within a virtual environment whenever using Python for projects. This keeps your dependencies for each project separate and organaized. Instructions for setting up a virual enviornment for your platform can be found in the [python docs](https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/)

#### PIP Dependencies

Once you have your virtual environment setup and running, install dependencies by naviging to the `/backend` directory and running:

```bash
pip install -r requirements.txt
```

This will install all of the required packages we selected within the `requirements.txt` file.

##### Key Dependencies

- [Flask](http://flask.pocoo.org/)  is a lightweight backend microservices framework. Flask is required to handle requests and responses.

- [SQLAlchemy](https://www.sqlalchemy.org/) is the Python SQL toolkit and ORM we'll use handle the lightweight sqlite database. You'll primarily work in app.py and can reference models.py. 

- [Flask-CORS](https://flask-cors.readthedocs.io/en/latest/#) is the extension we'll use to handle cross origin requests from our frontend server. 

## Database Setup
With Postgres running, restore a database using the trivia.psql file provided. From the backend folder in terminal run:
```bash
psql trivia < trivia.psql
```

## Running the server

From within the `backend` directory first ensure you are working using your created virtual environment.

To run the server, execute:

```bash
export FLASK_APP=flaskr
export FLASK_ENV=development
flask run
```

Setting the `FLASK_ENV` variable to `development` will detect file changes and restart the server automatically.

Setting the `FLASK_APP` variable to `flaskr` directs flask to use the `flaskr` directory and the `__init__.py` file to find the application. 

## Tasks

One note before you delve into your tasks: for each endpoint you are expected to define the endpoint and response data. The frontend will be a plentiful resource because it is set up to expect certain endpoints and response data formats already. You should feel free to specify endpoints in your own way; if you do so, make sure to update the frontend or you will get some unexpected behavior. 

1. Use Flask-CORS to enable cross-domain requests and set response headers. 
2. Create an endpoint to handle GET requests for questions, including pagination (every 10 questions). This endpoint should return a list of questions, number of total questions, current category, categories. 
3. Create an endpoint to handle GET requests for all available categories. 
4. Create an endpoint to DELETE question using a question ID. 
5. Create an endpoint to POST a new question, which will require the question and answer text, category, and difficulty score. 
6. Create a POST endpoint to get questions based on category. 
7. Create a POST endpoint to get questions based on a search term. It should return any questions for whom the search term is a substring of the question. 
8. Create a POST endpoint to get questions to play the quiz. This endpoint should take category and previous question parameters and return a random questions within the given category, if provided, and that is not one of the previous questions. 
9. Create error handlers for all expected errors including 400, 404, 422 and 500. 

REVIEW_COMMENT
```
This README is missing documentation of your endpoints. Below is an example for your endpoint to get all categories. Please use it as a reference for creating your documentation and resubmit your code. 

Endpoints
GET '/categories'
GET '/questions'
DELETE '/questions'
POST ...


GET '/categories'
- Fetches a dictionary of categories in which the keys are the ids and the value is the corresponding string of the category
- Request Arguments: None
- Returns: An object with a two keys, success and categories, that contains a key:value pairs of -> success: success boolean, categories: object of category_string key:value pairs. 
{
    'success': True,
    "categories": {'1' : "Science",
        '2' : "Art",
        '3' : "Geography",
        '4' : "History",
        '5' : "Entertainment",
        '6' : "Sports"}
}

GET '/questions'
- Fetches a list of questions in which the keys are the ids, questions, answers, category, and difficulty, and the value is the corresponding integer, string, string, integer, and integer respectively
- Fetches a dictionary of categories in which the keys are the ids and the value is the corresponding string of the category
- Fetches the current category as the category id integer
- If fetch unsuccessful becuase length of questions array is 0, returns the status code and an error object in which the keys are success, error, and message, and the values are the success boolean, error code, and message string respectively
- Fetches the total length of questions returned
- Request Arguments: None
- Returns: On success, an object with 5 keys, value pairs -> success: success boolean; questions: array of questions with each question an object containing -> id: question id integer, question: question question string, answer: question answer string, category: question category integer, difficulty: questions difficulty integer; total_questions: length of question array; categories: object containing category_string key:value pairs; current category: current category integer.
{
    'success': True
    'questions': [{'id': 25,
        'question': 'licks to get to the center of a tootsie pop',
        'answer': 'The world may never know',
        'category': 1,
        'difficulty': 1
    }, {'id': 2,
        'question': 'Where's waldo',
        'answer': 'Somewhere? Everywhere?',
        'category': 4,
        'difficulty': 5}],
    'total_questions': 2,
    'categories': {'1' : "Science",
        '2' : "Art",
        '3' : "Geography",
        '4' : "History",
        '5' : "Entertainment",
        '6' : "Sports"},
    'current_category': 'all'
}
- Returns: On failure, the error code and an object with 3 keys, value pairs -> 'success: success boolean; 'error': error code; "message": error message 
{
    "success": False,
    "error": 404,
    "message", "Not found"
}

DELETE '/questions/<int:id>'
- Deletes a question from the database where the question id is passed through the url as a variable
- If delete unsuccessful do to the provided questions id not existing in the database, returns the status code and an error object in which the keys are success, error, and message, and the values are the success boolean, error code, and message string respectively
- URL Variable Rules: question id integer
- Request Arguments: None
- Returns: on success, An object with a key, value pair of -> success: success boolean
{
    'success': True
}
- Returns: On failure, the error code and an object with 3 keys, value pairs -> 'success: success boolean; 'error': error code; "message": error message 
{
    "success": False,
    "error": 404,
    "message", "Not found"

Post '/questions'
- Adds a question to the database where the question question string, questions answer string, question difficulty integer, and question category integer are passed as request data
- If adding the question is unsuccessful because the difficulty integer is not between 0 and 5 or the question fails to insert into the database, returns the status code and an error object in which the keys are success, error, and message, and the values are the success boolean, error code, and message string respectively
- Request Arguments: an object containing key, value pairs of -> 'question': question string; 'answer': answer string; 'difficulty': difficulty integer; 'category': category integer
- Returns: on success, An object with a key, value pair of -> success: success boolean
{
    'success': True
}
- Returns: On failure, the error code and an object with 3 keys, value pairs -> 'success: success boolean; 'error': error code; "message": error message 
{
    "success": False,
    "error": 422,
    "message", "Unproccessable"

Post '/question_search'
- Fetches a list of questions in which the keys are the ids, questions, answers, category, and difficulty, and the value is the corresponding integer, string, string, integer, and integer respectively
- Fetches a dictionary of categories in which the keys are the ids and the value is the corresponding string of the category
- Fetches the current category as the category id integer
- Request Arguments: an object containing a key, value pair of -> 'searchTerm': search string
- Returns: on success, An object with a key, value pair of -> success: success boolean
{
    'success': True
    'questions': [{'id': 25,
        'question': 'licks to get to the center of a tootsie pop',
        'answer': 'The world may never know',
        'category': 1,
        'difficulty': 1
    }, {'id': 2,
        'question': 'Where's waldo',
        'answer': 'Somewhere? Everywhere?',
        'category': 4,
        'difficulty': 5}],
    'total_questions': 2,
    'current_category': 'all'
}

GET '/categories/<int:id>/questions'
- Fetches a list of questions in the category specified in the url in which the keys are the ids, questions, answers, category, and difficulty, and the value is the corresponding integer, string, string, integer, and integer respectively
- Fetches the total length of the questions list returned as an integer
- Fetches the current category as the category id integer
- Fetches the total length of questions returned
- If fetch unsuccessful becuase length of questions array is 0, returns the status code and an error object in which the keys are success, error, and message, and the values are the success boolean, error code, and message string respectively
- URL Variable Rules: category id integer
- Request Arguments: None
- Returns: On success, an object with 5 keys, value pairs -> success: success boolean; questions: array of questions with each question an object containing -> id: question id integer, question: question question string, answer: question answer string, category: question category integer, difficulty: questions difficulty integer; total_questions: length of question array; current category: current category integer.
{
    'success': True
    'questions': [{'id': 25,
        'question': 'licks to get to the center of a tootsie pop',
        'answer': 'The world may never know',
        'category': 1,
        'difficulty': 1
    }, {'id': 2,
        'question': 'Where's waldo',
        'answer': 'Somewhere? Everywhere?',
        'category': 4,
        'difficulty': 5}],
    'total_questions': 2,
    'categories': {'1' : "Science",
        '2' : "Art",
        '3' : "Geography",
        '4' : "History",
        '5' : "Entertainment",
        '6' : "Sports"},
    'current_category': 'all'
}
- Returns: On failure, the error code and an object with 3 keys, value pairs -> 'success: success boolean; 'error': error code; "message": error message 
{
    "success": False,
    "error": 404,
    "message", "Not found"
}

Post '/quizzes'
- Fetches a random question in the category specified in the request that is not in the list of previous questions specified in the request. question is returned as an object in which the keys are the ids, questions, answers, category, and difficulty, and the value is the corresponding integer, string, string, integer, and integer respectively
- If there are no more questions to return that are in the category specified in the request, and are not in the previous questions list specified in the request, None is returned for the "question" key.
- Request Arguments: an object containing a key, value pair of -> 'previous question': array of previous question integers; 'quiz_category': category integer
- Returns: On success, an object with 2 keys, value pairs -> success: success boolean; questions: a question object containing -> id: question id integer, question: question question string, answer: question answer string, category: question category integer, difficulty: questions difficulty integer; 
{
    'success': True
    'questions': {'id': 25,
        'question': 'licks to get to the center of a tootsie pop',
        'answer': 'The world may never know',
        'category': 1,
        'difficulty': 1}
}
Returns: On success where there are no remaining questions to return, an object with 2 keys, value pairs -> success: success boolean; questions: None
{
    'success': True
    'questions': None
}
```


## Testing
To run the tests, run
```
dropdb trivia_test
createdb trivia_test
psql trivia_test < trivia.psql
python test_flaskr.py
```