# 13 - Styling

## Finishing Touches

Now that we have our basic wire frame done we can start incorporating some style. This GitBook will not go too far deep into CSS, more so just get you started on how to load style sheets

Create a directory called static inside the students directory. Django will look for our css files here. Then inside of static, create another directory called students. Within that directory, create a CSS file called `style.css`.

Open up style.css inside the rabbit hole of the static directory and add the following code.

```text
h1 {
    border: solid;
}
```

Then head into landing.html and add this decorator to the very top of the file

`{% load static %}` 

Then add the link tag inside the head section of the file just above the title tag

```text
<link rel="stylesheet" type="text/css" href="{% static 'students/style.css' %}">
```

You may have to reload the server for this to go through. Press ctrl+c and run the command again inside terminal. Then refresh your browser to see the changes go through

