# 11 - Deleting Data

## The Routing

Add the following element to `students/urls.py`. 

`path('delete/<int:id>', students.views.delete, name='delete')` 

## The View

Add the following function to views.py

```text
def delete(request, id):
    student = Student.objects.get(id=id)

    if request.method == 'POST':
        student.delete()
        return redirect('index')

    return render(request, 'students/student_delete_confirm.html', {'student': student})
```

## The HTML

Create a new HTML file in templates/students and name it `student_delete_confirm.html`. Then add the following code

```text
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <form method="post">
        {% csrf_token %}
        <h2>Are you sure you want to remove</h2>
        <button type="submit">Confirm</button>
        <a href="{% url 'index' %}">Back</a>
    </form>
</body>
</html>
```

## Finally

Let's add a button to landing to navigate to the students section of our website. add the following snippet inside the div in landing.html after `{% endif %}`. 

 `<p><a href="{% url 'index' %}">Students</a></p>` 

## The Double Check

Run the server and play around with the buttons, make sure everything works, reads/writes to the database, etc.

