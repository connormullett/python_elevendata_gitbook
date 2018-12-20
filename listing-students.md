# 09 - Listing Students

## Creating the List View

Now that we have the ability to Create students and persist them to a database, let's work on listing those students in a view.

## Routing

Head over to `students/urls.py` and add the following element to `urlpatterns`.

`path('index', students.views.index, name='index')` 

## Views

Add the following function to `views.py` 

```text
def index(request):
    students = Student.objects.all()
    return render(request, 'students/students.html', {'students': students})
```

`.objects.all()` is a django property that acts as a sort of `GET ALL` . Because it already has access to the database, we can just tell it to snag everything, or pick and choose what we want it to show

Notice how we also pass students into a dictionary inside of the render function. This is what we will be iterating over in our HTML file. 

## The HTML

Create a new HTML file inside of templates/students called `students.html`. Then add the following code

```text
<html>
<head>
    <title>Students</title>
</head>
<body>
    <a href="{% url 'landing' %}">Home</a>
    <br>
    {% for student in students %}
    <p>Student ID: {{ student.id }}</p>
    <p>Last Name: {{ student.last_name }}</p>
    <p>First Name: {{ student.first_name }}</p>
    <p>GPA: {{ student.gpa }}</p>
    <a href="{% url 'update' student.id %}">Edit</a>
    <a href="{% url 'delete' student.id %}">Delete</a>
    {% endfor %}
    <br>
    <a href="{% url 'create' %}">New Student</a>
</body>
</html>
```

**Note:** Right now we won't be able to test because we have a couple errors. On line 13 and 14, we see a url that isn't defined yet. We will add these in during the next two sections

