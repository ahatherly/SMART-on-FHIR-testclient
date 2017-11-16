Simple test client for the SMART on FHIR standard using python
I have followed the steps outlined here: http://docs.smarthealthit.org/tutorials/authorization/

Setup
=====

First, create a python 3 virtual environment:

```
virtualenv -p /usr/bin/python3.4 smart-env
```

Now, activate your virtual environment and install the packages we need:

```
source smart-env/bin/activate
pip install requests-oauthlib flask
```

Now you can start the test client:

```
python app.py
```

It should now be running on http://localhost:5000/

Launching from the SMART sandbox
================================

To try it out, you'll need to create an account on https://sandbox.smarthealthit.org and create a test app entry.

Create your app entry in the sandbox using the "Register manually" button, with the following values:

 - App type: "Confidential Client"
 - App name: Anything
 - Launch URI: "http://localhost:5000/smart-app"
 - Redirect URIs: "http://localhost:5000/callback"

Make sure you update app.py with your client ID and secret (provided when you create the app in the sandbox).

Now, when you click the "Launch" button in the sandbox you should be able to select a patient, have it launch your app, authorise access, and then you should see a FHIR patient resource displayed from your app, which has been retrieved from the Smart Sandbox as part of an authenticated oauth2 session.

Standalone Launch
=================

The other way of launching a SMART on FHIR app is as a standalone launch. In this case the app needs to know the resource server URL so it can get the CapabilityStatement and find the auth URL. In our example, this is hard-coded to the SMART sandbox URL, so if you want to test against a different server you'll need to change the URL in app.py.

To try this out, launch http://localhost:5000 and click the standalone login link.

