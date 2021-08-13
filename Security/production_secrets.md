# Production secrets
Usually in every project you can find many usernames, passwords and tokens to access to different services.

If those secret keys are stolen, an attacker can access your related services, then can steal or destroy more data, or leave a nasty surprise on your credit card, for example by abusing a paid API service.

Therefore, it is a good idea to separate these keys from the rest of the code in your project.

There are mainly two approaches to this:
* create a separate **secrets file**
* save the secret keys as **environment variables**

***
## Secrets file
Lets sopouse we have these secrets:
* EMAIL_HOST_USER
* EMAIL_HOST_PASSWORD

Create a file named **secrets.py**

```python
# secrets.py
EMAIL_HOST_USER='user@my_mail.server'
EMAIL_HOST_PASSWORD='my_password'
```
Then you can import these variables in your code with:

```python
from .secrets import *
print(EMAIL_HOST_USER)
```

### Gitinore the secrets.py file
add a file named **.gitignore** at the root of your project, and put inside the name of the file to ignore: **secrets.py**

    # .gitignore
    secrets.py

### Make a template for the secrets file
The secrets file will be left out from the version control. So its a good idea to save a template, in case your teammates, or yourself in the future, don't know which variables need to be set. Create a file named **secrets.py.template** and make a template for the keys, this file will be saved by git.

```python
# secrets.py.template
EMAIL_HOST_USER='complete my user here '
EMAIL_HOST_PASSWORD='complete my password here'
```


***
## Environment variables
In unix-like systems you can set your enviroment variables like this:

    $ export EMAIL_HOST_USER='user@my_mail.server'
    $ export EMAIL_HOST_PASSWORD='my_password'

These will be valid until the end of the session. A better approach is to add them to the **~/.bashrc** file, to make the system load them everytime you open a terminal session:

Many cloud services like Heroku have the option to set environment variables, for every instance of their services.


***
## Mixed approach
* on development SECRET_KEY is  in secrets.py (gitignored)
* on deployment SECRET_KEY is an environment variable

```python
import os
[...]
try:
    # on development SECRET_KEY is  in secrets.py (gitignored)
    from .secrets import *
except ModuleNotFoundError:
    # on deployment SECRET_KEY is an environment variable
    EMAIL_HOST_USER = os.environ.get('EMAIL_HOST_USER')
    EMAIL_HOST_PASSWORD = os.environ.get('EMAIL_HOST_PASSWORD')
```
