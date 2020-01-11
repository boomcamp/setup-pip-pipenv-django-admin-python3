# Basic environment set-up.

- Switching from python 2 to python 3 version.
- Installing pipenv using pip3.
- Installing dependencies using pipenv.
- Creating a starter project using django-admin.
- Running the basic migration with SQLite.
- Creating a super user account.

### Switching python 2 into python 3 version.

Python 2 will be no longer maintain until 2020, so its ideal if we switch to it's newer version you can read more about 

- [Python 2.7 will retire in](https://pythonclock.org/).
- [Article about python's end of life](https://www.anaconda.com/end-of-life-eol-for-python-2-7-is-coming-are-you-ready/).

1. First we need to check the available versions of python.

```
ls /usr/bin/python*
```

It will display the python version's installed in your computer:

```
dev-mentor@devmentor-PC-MK34LEZCBEAD:~$ ls /usr/bin/python*
/usr/bin/python     /usr/bin/python3           /usr/bin/python3.6m         /usr/bin/python3.7m      /usr/bin/python3m-config
/usr/bin/python2    /usr/bin/python3.6         /usr/bin/python3.6m-config  /usr/bin/python3-config
/usr/bin/python2.7  /usr/bin/python3.6-config  /usr/bin/python3.7          /usr/bin/python3m
```
if havent installed python 3 : [Install-python-3-7-on-ubuntu-18-04](https://linuxize.com/post/how-to-install-python-3-7-on-ubuntu-18-04/).

2. Next edit `./bashrc`.

```
sudo nano ~/.bashrc
```

3. Set alias for `python` and point the version you may want in this case `python3.7`.

```
alias python='/usr/bin/python3.7'
```

3. Reload the `.bashrc`.

```
source ~/.bashrc
```

3. Finally we can check the new version.

```
dev-mentor@devmentor-PC-MK34LEZCBEAD:~$ python --version
Python 3.7.4
```


### Installing pipenv using pip3.

[Python pip](https://realpython.com/what-is-pip/) is a package manager for Python.

Installation:

```
sudo apt install python3-pip
#for python 2: sudo apt install python-pip
```

### Setting alias pip3 as pip

1. Find the `pip3` path.

```
dev-mentor@devmentor-PC-MK34LEZCBEAD:~/Downloads/my-app$ whereis pip3
pip3: /usr/bin/pip3 /home/dev-mentor/.pyenv/shims/pip3.7 /home/dev-mentor/.pyenv/shims/pip3 /usr/share/man/man1/pip3.1.gz
```

2. After that we need to update our `.bashrc`.

```
sudo nano ~/.bashrc 
```

and set alias `pip` by pointing its path.

```
alias pip='/usr/bin/pip3'
```

3. Reload shell

```
source ~/.bashrc 
```

4. Done !

```
dev-mentor@devmentor-PC-MK34LEZCBEAD:~/Downloads/my-app$ pip --version
pip 9.0.1 from /usr/lib/python3/dist-packages (python 3.6)
```

### Installing pipenv

[Pipenv](https://pypi.org/project/pipenv/) is a tool that aims to bring the best of all packaging worlds (bundler, composer, npm, cargo, yarn, etc.)

```
sudo pip3 install pipenv
#for python 2 version: sudo pip install pipenv
```

Check both versions. 

```
dev-mentor@devmentor-PC-MK34LEZCBEAD:~$ pip --version
pip 9.0.1 from /usr/lib/python3/dist-packages (python 3.6)
dev-mentor@devmentor-PC-MK34LEZCBEAD:~$ pipenv --version
pipenv, version 2018.11.26
```

### Installing project dependencies using pipenv.

1. First we need to create our project container called `my-app`.

```
mkdir my-app && cd my-app
```

2. We also need to initialize our virtual environment.

```
pipenv --three
```

3. Install `python3`.

```
pipenv --python 3.7
```

4. Install [Django](`https://www.djangoproject.com/download/`).

```
pipenv install Django==2.2.6
```

5. Activate the virtual environment.

```
pipenv shell
```

Done:

```
(my-app) dev-100@dev100-PC-MK34LEZCBEAD:~/Downloads/my-app$
Pipfile  Pipfile.lock
```

**(my-app)** = Our active virtual environment.

**Pipfile** =  Handles the virtual environment packages and settings.


Our created Pipfile:

```
[[source]]                          # Here goes your package sources (where you are downloading your packages from).
name = "pypi"
url = "https://pypi.org/simple"
verify_ssl = true

[dev-packages]                      # The required development packages

[packages]                          # The required package to run application
django = "==2.2.6"                 

[requires]                          # The required python version
python_version = "3.6"             
```

Example of what we have installed in `(my-app)` environment:


![An image of packages](available-packages-in-my-app-environment.png)


## Creating starter project with django-admin.

**django-admin** = is a ready-to-use user interface for administrative activities. We all know how an admin interface is important for a web project. Django automatically generates admin UI based on your project models.[Tutorialspoint](https://www.tutorialspoint.com/django/django_admin_interface.htm).

[Read more: Django 2.2](https://docs.djangoproject.com/en/2.2/ref/contrib/admin/)

6. We can check django version.

```
django-admin --version
```

7. Initialize django project called `sample`.

```
django-admin startproject sample
```

We should have now this basic folder and files structure, you can read the explanation [here](https://django-project-skeleton.readthedocs.io/en/latest/structure.html):

```
(my-app) dev-mentor@devmentor-PC-MK34LEZCBEAD:~/Downloads/my-app$ tree
.
├── Pipfile
├── Pipfile.lock
└── sample
    ├── manage.py
    └── sample
        ├── __init__.py
        ├── settings.py
        ├── urls.py
        └── wsgi.py

2 directories, 7 files
```

8. Next change directory to our created project folder.

```
cd sample
```

9. We can now run our application using `python3`.

```
python manage.py runserver
```

Output:

```
(my-app) dev-100@dev100-PC-MK34LEZCBEAD:~/Downloads/my-app$ python3 manage.py runserver
Performing system checks...

System check identified no issues (0 silenced).

You have 13 unapplied migration(s). Your project may not work properly until you apply the migrations for app(s): admin, auth, contenttypes, sessions.
Run 'python manage.py migrate' to apply them.

October 04, 2019 - 06:20:18
Django version 1.11.25, using settings 'test_project.settings'
Starting development server at http://127.0.0.1:8000/
Quit the server with CONTROL-C.
```


### You should now see this default welcome page

Host: `http://127.0.0.1:8000/`

![An image of welcome landing page](landing-page.png)

`ctrl+d` = Will exit (my-app) virtual environment.

`ctrl+c` = Quit server.


## Running basic migration with SQLite.

By default, the configuration uses *SQLite*, you can type `python3 manage.py migrate` to create tables, the output will be:

```
(my-app) dev-100@dev100-PC-MK34LEZCBEAD:~/Downloads/my-app/sample$ python manage.py migrate
Operations to perform:
  Apply all migrations: admin, auth, contenttypes, sessions
Running migrations:
  Applying contenttypes.0001_initial... OK
  Applying auth.0001_initial... OK
  Applying admin.0001_initial... OK
  Applying admin.0002_logentry_remove_auto_add... OK
  Applying admin.0003_logentry_add_action_flag_choices... OK
  Applying contenttypes.0002_remove_content_type_name... OK
  Applying auth.0002_alter_permission_name_max_length... OK
  Applying auth.0003_alter_user_email_max_length... OK
  Applying auth.0004_alter_user_username_opts... OK
  Applying auth.0005_alter_user_last_login_null... OK
  Applying auth.0006_require_contenttypes_0002... OK
  Applying auth.0007_alter_validators_add_error_messages... OK
  Applying auth.0008_alter_user_username_max_length... OK
  Applying auth.0009_alter_user_last_name_max_length... OK
  Applying auth.0010_alter_group_name_max_length... OK
  Applying auth.0011_update_proxy_permissions... OK
  Applying sessions.0001_initial... OK
(my-app) dev-100@dev100-PC-MK34LEZCBEAD:~/Downloads/my-app/sample$ 
```

### Creating a super user.

1. After a successfull migration, you may want to create superuser.

```
python manage.py createsuperuser
```

It will ask basic details for superuser account.

```
(my-app) dev-100@dev100-PC-MK34LEZCBEAD:~/Downloads/my-app/sample$ python3 manage.py createsuperuser
Username (leave blank to use 'dev-100'): admin
Email address: jino.lacson@boom.camp
Password: 
Password (again): 
Superuser created successfully.
```

2. After that serve the application folder.

```
python manage.py runserver
```

3. Next navigate to admin dashboard, you should now able to login as superuser account.

```
http://127.0.0.1:8000/admin #http://127.0.0.1:8000/admin/login/?next=/admin/
```

### Super admin panel after successfull logged in and migration:

![An image of admin panel](super-admin-panel.png)


# Next

Django-rest-framework: https://github.com/boomcamp/django-restframework

