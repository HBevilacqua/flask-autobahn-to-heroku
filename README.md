# Flask & Autobahn to Heroku

[![Deploy](https://www.herokucdn.com/deploy/button.svg)](https://heroku.com/deploy)

This is a template project for running a Flask web app using Autobahn WAMP implementation. Everything can be ran on Heroku or somewhere else.

This is somewhat based on [AutobahnPython Crochet examples](https://github.com/crossbario/autobahn-python/tree/master/examples/twisted/wamp/app/crochet).
 * The web application (`webapp.py`) performs synchronous RPC calls and publishes topics.
 * The backend (`backend.py`) registers RPC procedures and subscribes to topics.

![screencast](https://raw.githubusercontent.com/AndreMiras/flask-autobahn-to-heroku/master/static/images/screencast.gif)

In the above screencast, we start by running the one-off backend dyno on Heroku. Then clicking to the web app links performs Remote Procedure Calls and events publish, all handled by the backend. Values returned by the backend are received by the web app and displayed to the HTML page.

## Deploy
Deploy the web application on Heroku automatically using the "Deploy to Heroku" button.

The `ROUTER_ADDRESS` environment variable must be set to a Crossbar.io router running a reaml called `realm1`, like the one provided in [AndreMiras/crossbar-hello-python-to-heroku](https://github.com/AndreMiras/crossbar-hello-python-to-heroku).

If you haven't done so using the "Deploy to Heroku" button, do it from your term.
```
heroku config:set ROUTER_ADDRESS=wss://some.crossbar.router.address/ws
```
It also applies if you run the application locally.
```
export ROUTER_ADDRESS=wss://some.crossbar.router.address/ws
```

## Play
Run the backend using a [one-off dyno](https://devcenter.heroku.com/articles/one-off-dynos).
```
heroku run python backend.py
```
Or run it on your local computer or any other divice.
```
python backend.py
```
Then open your web browser to the deployed Heroku application to talk to the backend.

## Shutdown
Stop your dynos if you don't want to get charged.
```
heroku ps:scale web=0
```
