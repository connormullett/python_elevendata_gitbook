# 08 - Create Functionality

## Giving Access To New URLs

Look into `eleven_data/urls`. Notice in the path function with `'accounts/'` as a parameter, we see include after it. This tells django to go down a rabbit hole to match a URL. We can use this to separate our urls into more legible and accessible chunks. We will be doing this for the rest of our app. Add the following element to \`urlpatterns'

```text
path('students/', include('students.urls'))
```

Remember that Django will always go through the _project_ \(in our case eleven\_data/urls\) url file first.

## Routing

For our create view we are going to add the following element to students/urls. This way when we add `students/create`, it will navigate us to the create view. 

```text
from django.urls import path
import students.views

urlpatterns = [
    path('create', students.views.create, name='create')
]
```

## The HTML

Inside of the students templates subdirectory, add the following code to a new HTML file named \`student\_form.html'.

![](.gitbook/assets/student_form_template%20%281%29.png)

## The View

Slap the following function into views.py 

```text
def create(request):
    form = StudentForm(request.POST or None)

    if form.is_valid():
        form.save()
        return redirect('index')

    if request.method == "GET":
        return render(request, 'students/student_form.html', {'form': form})
```

On line 2 of the code snippet, we see something peculiar. We are instantiating an object, but does it belong to django? The answer is no, we need to build it out. Create a new Python file inside of the students app directory and call it `forms.py`. Then add the following code to the newly created file.

```text
from django import forms
from .models import Student


class StudentForm(forms.ModelForm):
    class Meta:
        model = Student
        fields = ('first_name', 'last_name', 'gpa')
```

This binds the form to specific fields with certain values that we want. This way its more modular and we can pass in information from the view function.

After that head back to views.py. We should still see an error, that's because we still don't have the module imported. Add the following line to views.py to kick over the new form object we created.

 `from .forms import StudentForm` 

## Double Check

Now's a good time to stop and make sure everything is working. Run the development server and navigate to /students/create. Then try to create a student. If you see the student in PGAdmin, then you can move on to the next step.

