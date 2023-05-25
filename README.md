# To-Do List Application

This Python application is a simple implementation of a To-Do list web app using the microdot_asyncio library.

## Imports and setup:
```
from microdot_asyncio import Microdot, Response

app = Microdot()
Response.default_content_type = 'text/html'
```
The microdot_asyncio library provides a lightweight, asynchronous, and fast API framework. Microdot is a class for creating an application object, and Response is used to handle HTTP responses. We then create an instance of the Microdot class, representing our web application, and set the default content type of HTTP responses to text/html.

## Data storage:

``todos = []``

This is a list used to store our tasks or "to-dos". Each task is a list containing three items: a boolean indicating if the task is completed, the name of the task, and its priority.

## HTML generation:

```
def htmldoc():
    todo_list = ''.join([f'<li>{todo[1]} - Priority: {todo[2]} - <a href="/toggle/{i}">{"Complete" if not todo[0] else "Uncomplete"}</a> - <a href="/delete/{i}">Delete</a></li>' for i, todo in enumerate(todos)])

    return f
        <!-- HTML content here -->
```        
This function generates HTML content for our webpage. The todo list is generated dynamically based on the todos list.

## Routes and handling requests:

``@app.route('/', methods=['GET', 'POST'])
async def home(request):
    if request.method == 'POST':
        todos.append([False, request.form.get('task'), request.form.get('priority')])
    return htmldoc()``


``@app.route('/add', methods=['POST'])
async def add(request):
    todos.append([False, request.form.get('task'), request.form.get('priority')])
    return htmldoc()``


``@app.route('/toggle/<index>')
async def toggle(request, index):
    todos[int(index)][0] = not todos[int(index)][0]
    return htmldoc()``


``@app.route('/delete/<index>')
async def delete(request, index):
    todos.pop(int(index))
    return htmldoc()``
    
These are the routes that our application handles. The home route accepts both GET and POST methods. When a POST request is received, a new task is added to our todos list. The add route also accepts a POST request to add a new task. The toggle route toggles the status of a task between completed and uncompleted, and the delete route removes a task from the list.

## Running the app:

``app.run(debug=True, port=8008)``

Finally, we run our application on port 8008 with debug mode enabled.

For more information on microdot_asyncio, please visit the official microdot_asyncio documentation.
