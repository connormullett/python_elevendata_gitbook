# 12 - Happy Little Decorator

## **Validating and Restricting Users**

Django comes with a couple decorators that allows us to easily add extra functionality. The one we'll be using for this app is `@login_required`. We can put this function decorator above our view functions to limit users who are not logged in. All we have to do is add it above the function like so

```text
from django.contrib.auth.decorators import login_required

@login_required <--
def create(request):
```

Run the server, log out of any existing account, and try to create a new student. It will redirect you to the login page. What's pretty cool about this is it stores the page you are trying to access in the `request` object's `next` variable. So after we login we can continue on like nothing happened.

