# Django Test
This is going through the official django tutorial [here](https://docs.djangoproject.com/en/2.1/intro/tutorial01/).

## Notes
Commands to set this up on Fedora 29:
```bash
pip3 install pip --upgrade --user
pip3 install virtualenv --user
cd $REPO_ROOT
virtualenv env
source env/bin/activate
pip install django
django-admin startproject testsite .
python manage.py startapp polls
pip freeze > requirements.txt
```