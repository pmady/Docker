Install psycopg2-binary With Docker


How to build a Python app with PostgreSQL

I’m currently setting up a Flask app with PostgreSQL and Docker.

Like most examples you’ll find on the internet, the course I’m following uses Alpine Linux as a base image. Alpine’s selling point is the small image size.

But Alpine uses a different C library, musl, instead of glibc.

That’s one of the reasons why the website Pythonspeed recommends Debian Buster as the base image for Python (as of 2019).

Let’s say we have a requirements.txt file with the following packages. We want to get Flask working with a PostgreSQL database.


#Docker  #Linux  #DevOps  #DevTools  #Python 
