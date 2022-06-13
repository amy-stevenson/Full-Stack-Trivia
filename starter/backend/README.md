# Backend - Full Stack Trivia API 

### Installing Dependencies for the Backend

1. **Python 3.7** - Follow instructions to install the latest version of python for your platform in the [python docs](https://docs.python.org/3/using/unix.html#getting-and-installing-the-latest-version-of-python)


2. **Virtual Enviornment** - We recommend working within a virtual environment whenever using Python for projects. This keeps your dependencies for each project separate and organaized. Instructions for setting up a virual enviornment for your platform can be found in the [python docs](https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/)


3. **PIP Dependencies** - Once you have your virtual environment setup and running, install dependencies by naviging to the `/backend` directory and running:
```bash
pip install -r requirements.txt
```
This will install all of the required packages we selected within the `requirements.txt` file.


4. **Key Dependencies**
 - [Flask](http://flask.pocoo.org/)  is a lightweight backend microservices framework. Flask is required to handle requests and responses.

 - [SQLAlchemy](https://www.sqlalchemy.org/) is the Python SQL toolkit and ORM we'll use handle the lightweight sqlite database. You'll primarily work in app.py and can reference models.py. 

 - [Flask-CORS](https://flask-cors.readthedocs.io/en/latest/#) is the extension we'll use to handle cross origin requests from our frontend server. 

### Database Setup
With Postgres running, restore a database using the trivia.psql file provided. From the backend folder in terminal run:
```bash
psql trivia < trivia.psql
```

### Running the server

From within the `./src` directory first ensure you are working using your created virtual environment.

To run the server, execute:

```bash
flask run --reload
```

The `--reload` flag will detect file changes and restart the server automatically.

## ToDo Tasks
These are the files you'd want to edit in the backend:

1. *./backend/flaskr/`__init__.py`*
2. *./backend/test_flaskr.py*


One note before you delve into your tasks: for each endpoint, you are expected to define the endpoint and response data. The frontend will be a plentiful resource because it is set up to expect certain endpoints and response data formats already. You should feel free to specify endpoints in your own way; if you do so, make sure to update the frontend or you will get some unexpected behavior. 

1. Use Flask-CORS to enable cross-domain requests and set response headers. 


2. Create an endpoint to handle GET requests for questions, including pagination (every 10 questions). This endpoint should return a list of questions, number of total questions, current category, categories. 


3. Create an endpoint to handle GET requests for all available categories. 


4. Create an endpoint to DELETE question using a question ID. 


5. Create an endpoint to POST a new question, which will require the question and answer text, category, and difficulty score. 


6. Create a POST endpoint to get questions based on category. 


7. Create a POST endpoint to get questions based on a search term. It should return any questions for whom the search term is a substring of the question. 


8. Create a POST endpoint to get questions to play the quiz. This endpoint should take category and previous question parameters and return a random questions within the given category, if provided, and that is not one of the previous questions. 


9. Create error handlers for all expected errors including 400, 404, 422 and 500. 


## API Documentation

GET `\categories`
- Fetches a dictionary of categories in which the keys are the ids and the value is the corresponding string of the category
- Request parameters: none
- Example response:
```
{
  "categories": {
    "1": "Science", 
    "2": "Art", 
    "3": "Geography", 
    "4": "History", 
    "5": "Entertainment", 
    "6": "Sports"
  }, 
  "success": true
}

```


GET `\questions?page=<page_number>`
- Fetches a paginated set of questions, a total number of questions, all categories and current category string.
- Request parameters (optional): page:int
- Example response:
 ``` {
  "categories": {
    "1": "Science", 
    "2": "Art", 
    "3": "Geography", 
    "4": "History", 
    "5": "Entertainment", 
    "6": "Sports"
  }, 
  "current_category": null, 
  "questions": [
    {
      "answer": "Maya Angelou", 
      "category": 4, 
      "difficulty": 2, 
      "id": 5, 
      "question": "Whose autobiography is entitled 'I Know Why the Caged Bird Sings'?"
    },  
    {
      "answer": "Tom Cruise", 
      "category": 4, 
      "difficulty": 5, 
      "id": 4, 
      "question": "What actor did author Anne Rice first denounce, then praise in the role of her beloved Lestat?"
    }
  ], 
  "success": true, 
  "total_questions": 2
}
```

DELETE `/questions/<question_id>`
- Deletes a specified question using the id of the question
- Request arguments: question_id:int
- Example response:
```
{
  "deleted": "8", 
  "success": true
}
```

POST `/questions`
- Sends a post request in order to add a new question
- Request body: {question:string, answer:string, difficulty:int, category:string}
- Example response:
```
{
  "created": 11, 
  "success": true
}
```
POST `/questions/search`
- Sends a post request in order to search for a specific question by search term
- Request body: {searchTerm:string}
- Example response:
```
{
  "current_category": null, 
  "questions": [
    {
      "answer": "Waldo", 
      "category": 5, 
      "difficulty": 2, 
      "id": 88, 
      "question": "Who is hard to find?"
    }
  ], 
  "success": true, 
  "total_questions": 1
}
```

GET `/categories/<int:category_id>/questions`
- Fetches questions for a cateogry specified by id request argument
- Request argument: category_id:int
- Example response:
```
{
  "current_category": 1, 
  "questions": [
    {
      "answer": "Brazil", 
      "category": 1, 
      "difficulty": 3, 
      "id": 10, 
      "question": "Which is the only team to play in every soccer World Cup tournament?"
    }, 
    {
      "answer": "Muhammad Ali", 
      "category": 1, 
      "difficulty": 1, 
      "id": 9, 
      "question": "What boxer's original name is Cassius Clay?"
    }, 
  ], 
  "success": true, 
  "total_questions": 2
}
```
POST `/quizzes`
- Sends a post request in order to get the next question
- Request body: {previous_questions: arr, quiz_category: {id:int, type:string}}
- Example response:
```
{
  "question": {
    "answer": "Apollo 13 ", 
    "category": 5, 
    "difficulty": 4, 
    "id": 2, 
    "question": "What movie earned Tom Hanks his third straight Oscar nomination, in 1996?"
  }, 
  "success": true
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
