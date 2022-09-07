# Standalone Google Recaptcha for Python
Google recaptcha helps you protect your web form by using google's latest recaptcha 
(Completely Automated Public Turing test to tell Computers and Humans Apart) technology.

[![PyPi](https://github.com/jpraychev/google-recaptcha/actions/workflows/python-publish.yml/badge.svg)](https://github.com/jpraychev/google-recaptcha/actions/workflows/python-publish.yml)
[![PyPI Downloads](https://img.shields.io/pypi/dm/google-recaptcha.svg)](https://pypistats.org/packages/google-recaptcha)

# Documentation

# Installation
```
pip install google-recaptcha
```

# Introduction
Current version of the library works by placing the {{ recaptcha }} object in the form you want to protect. It searches automatically for the form that the object is placed in.

In your views file with RECAPTCHA_SITE_KEY and RECAPTCHA_SECRET_KEY exported as environment variables.

```
# With environment variables

from google_recaptcha import ReCaptcha
app = Flask(__name__)
recaptcha = ReCaptcha(app=app)

@app.route("/contact/", methods=["GET", "POST"])
def home():

    if recaptcha.verify():
        print('Recaptcha has successded.')
    else:
        print('Recaptcha has failed.')
```

```
# Without environment variables
from google_recaptcha import ReCaptcha
app = Flask(__name__)
recaptcha = ReCaptcha(
    app=app,
    site_key="your-site-key",
    secret_key="your-secret-key"
)

@app.route("/contact/", methods=["GET", "POST"])
def home():

    if recaptcha.verify():
        print('Recaptcha has successded.')
    else:
        print('Recaptcha has failed.')
```
In your HTML template file:
```
<form id="contact-form" method="post" class="control-form">
    <div class="row">
        <div class="col-xl-6">
            <input type="text" name="name" placeholder="Name" required="" id="id_name">
        </div>
        <div class="col-xl-6">
            <input type="text" name="email" placeholder="Email" required="" id="id_email">
        </div>
        <div class="col-xl-12">
            <input type="text" name="subject" placeholder="Subject" required="" id="id_subject">
        </div>
        <div class="col-xl-12">
            <textarea name="message" cols="40" rows="10" placeholder="Message" required="" id="id_message"></textarea>
        </div>
        <div class="col-xl-12">
            <button id="form-btn" type="submit" class="btn btn-block btn-primary">Send now</button>
        </div>
    </div>
    {{ recaptcha }}
</form>
```