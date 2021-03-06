# Circulate - Demo App for CircleCI

Credit: This is directly based on Miguel Grinberg's excellent [Flasky](https://github.com/miguelgrinberg/flasky) application.[![CircleCI](https://circleci.com/gh/CircleCI-Public/circleci-demo-python-flask.svg?style=svg&circle-token=6715e4f37e6b8cee04ea7f1812ac00fb135199f9)](https://circleci.com/gh/CircleCI-Public/circleci-demo-python-flask/)

This is a working application using Python and Flask that you can use to learn how to build, test and deploy with CircleCI 2.0. Follow the [Project Walkthrough](https://circleci.com/docs/2.0/project-walkthrough/) guide here.

It's a 'social blogging' web application similar to Twitter. Users can create accounts, make posts, follow users and comment on posts. You can *circualate* your thoughts and ideas :-)

**IMPORTANT:**

- You **do not need to know Python to follow the guide** in the CircleCI docs.
- You will not need to install or setup a Python environment to follow the tutorial - you can follow along by making edits to config on GitHub if you wish.
- No matter what language or stack you are going to use with CircleCI, we recommend following the [walkthrough](https://circleci.com/docs/2.0/project-walkthrough/) first, as it introduces concepts about CircleCI that you can then apply to your own project.

# Running locally
**Note:** As mentioned above you don't need to run this application locally to learn about using CircleCI.

## 1. Setup your Local Environment & Clone the Circulate Repo

The following commandline instructions are for Mac users. For other operating systems, install Postgres with [these](https://www.postgresql.org/download/) instructions, and Python using [these](https://www.python.org/downloads/) instructions.

### Install Postgres
`brew install postgres`

### Install Python
`brew install python`

### Fork or clone this repository
`git clone git@github.com:CircleCI-Public/circleci-demo-python-flask.git`

### Create and activate a virtual environment

```python3 -m venv venv-name```

```source venv-name/bin/activate```

**Note** For Ubuntu Linux, use `sudo apt-get install python3-venv`.

## 2. Initialize your PostgreSQL database
`createdb circulate`

## 3. Install your dependencies
`pip install -r requirements/dev.txt`

## 4. Use the `manage.py` script to operate the app

### Seed database and create tables with the `deploy` argument
```
python manage.py deploy
```
Your output should show:
```
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
```

### Run Circulate's server and deploy locally with the `runserver` argument
`python manage.py runserver`

Next, we'll show you how to test the app locally with the Flask development server.

### Run tests with the `test` argument
```python manage.py test```

#### Test report generation
This demo uses [unittest-xml-reporting](https://github.com/xmlrunner/unittest-xml-reporting) for JUNIT style report generation.

#### Unit Tests
Unit testing was applied to:
- database models (using [unittest](https://docs.python.org/3.7/library/unittest.html))
- client view functions (using [Flask Test Client](http://flask.pocoo.org/docs/1.0/testing/))
- API (using [Flask Test Client](http://flask.pocoo.org/docs/1.0/testing/))

#### Integration Tests

Integration testing is completed for logging in, etc, using [Selenium](https://www.seleniumhq.org/) and [ChromeDriver](http://chromedriver.chromium.org/).

## 5. Deployment to Heroku

The application also demonstrates how to deploy to Heroku from CircleCI 2.0. Please consult the [Project Walkthrough](https://circleci.com/docs/2.0/project-walkthrough/) for documentation on how this works.

## TODO

- add registration button on homepage
- add [parallelization](https://circleci.com/docs/2.0/parallelism-faster-jobs/)
- test with multiple python versions (3.6.2 and 3.7.1 currently tested)
- run with coverage on CircleCI
- make email testing work on CircleCI with mailhog
- Add authentication/login
- fix email verification upon registration "A confirmation email has been sent to you by email."
```
2018-11-20T22:19:14.576584+00:00 app[web.1]: raise err
2018-11-20T22:19:14.576586+00:00 app[web.1]: File "/app/.heroku/python/lib/python3.7/socket.py", line 716, in create_connection
2018-11-20T22:19:14.576588+00:00 app[web.1]: sock.connect(sa)
2018-11-20T22:19:14.576590+00:00 app[web.1]: ConnectionRefusedError: [Errno 111] Connection refused
2018-11-20T22:19:14.576591+00:00 app[web.1]:
2018-11-20T22:19:14.576876+00:00 app[web.1]: 10.11.245.78 - - [20/Nov/2018:22:19:14 +0000] "POST /auth/register HTTP/1.1" 302 229 "https://joiahdh.herokuapp.com/auth/register" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_13_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/70.0.3538.102 Safari/537.36"
```
- fix forgot password "An email with instructions to reset your password has been sent to you."
- make email work on the deployed Heroku app
- fill out test details: See the `tests` directory for details.

---
