# Putting it All Together: Client-Server Communication

## Learning Goals

- Understand how to communicate between client and server using fetch, and how
  the server will process the request based on the URL, HTTP verb, and request
  body
- Debug common problems that occur as part of the request-response cycle

## Introduction

Just like the last lesson, we've got code for a React frontend and Rails API
backend set up. This time though, it's up to you to use your debugging skills to
find and fix the errors!

To get the backend set up, run:

```console
$ bundle install
$ rails db:migrate db:seed
$ rails s
```

Then, in a new terminal, run the frontend:

```console
$ npm install --prefix client
$ npm start --prefix client
```

Confirm both applications are up and running by visiting
[`localhost:4000`](http://localhost:4000) and viewing the list of toys in your
React application.

## Deliverables

In this application, we have the following features:

- Display a list of all the toys
- Add a new toy when the toy form is submitted
- Update the number of likes for a toy
- Donate a toy to Goodwill (and delete it from our database)

The code is in place for all these features on our frontend, but there are some
problems with our API! We're able to display all the toys, but the other three
features are broken.

Use your debugging tools to find and fix these issues.

There are no tests for this lesson, so you'll need to do your debugging in the
browser and using the Rails server logs and `byebug`.

**Note**: You shouldn't need to modify any of the React code to get the
application working. You should only need to change the code for the Rails API.

As you work on debugging these issues, use the space in this README file to take
notes about your debugging process. Being a strong debugger is all about
developing a process, and it's helpful to document your steps as part of
developing your own process.

## Your Notes Here

- Add a new toy when the toy form is submitted

  - How I debugged:
    - I tried to submit an empty form
    - I looked in the Network tab on the brower and saw a 500 Internal Server Error
    - So I went in my Rails server log to look for the last request and see what the error is: NameError (uninitialized constant ToysController::Toys):
    - I can see that the error is Toys in my ToysController so I fix it and changed it to Toy
    - I try to submit the form again: success!

- Update the number of likes for a toy

  - How I debugged:
    - I tried to like a toy
    - I can see an Unexpected end of JSON input error in the browser console
    - I checked your fetch request
    - I check the controller action to make sure to render json: it wasn't the case so I added it
    - I tried to like a toy again: success!

- Donate a toy to Goodwill (and delete it from our database)

  - How I debugged:
    - I tried to delete a toy
    - I can see a 404 Not Found Error in the Network tab in the frontend
    - So I checked my Rails server log in the backend and see this error message: ActionController::RoutingError (No route matches [DELETE] "/toys/1"):
    - I can see that there is no delete route so I added it to handle the http verb and path for that request: adding :destroy in resources for toys
    - I tried to delete a toy again: success!
