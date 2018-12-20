# 10 - Updating Existing Information

## Routing

Add the following element to `students/urls.py`

`path('update/<int:id>', views.update, name='update')`

Time for some new syntax. `<int:id>`. Remember that Python is dynamically typed meaning that we don't have to declare data types, so this is kind of scary. This is what python calls _type hinting_. This tells the url to _expect_ an integer and save it under the name id. In our future view functions we need a new parameter that will automatically be passed in to represent this id. The id here is what's called a primary key. If we open PGAdmin and inspect any of our tables, we see `id` at the left most column, and then right under it, we see \[PK\]. Primary keys are unique table identifiers that can be queried on for specific information. In this case, when we list out our students, we are also getting the primary key from the database. This is where its coming from.

## The View

As stated earlier, we need a new parameter. Add the following function to your views.py.

```text
def update(request, id):
    student = Student.objects.get(id=id)
    form = StudentForm(request.POST or None, instance=student)

    if form.is_valid():
        form.save()
        return redirect('index')

    return render(request, 'students/student_form.html', {'form': form, 'student': student})
```

## The HTML

We don't need any html for updating. If we look into `students/student_form.html` we have already used it before. We are just passing in the data from the dictionary in `render` to the form so we can update it there.

 

