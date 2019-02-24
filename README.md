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

DB commands:
```bash
# Make all
python manage.py makemigrations
# Make just polls
python manage.py makemigrations polls
# See what a specific migration will do to the db
python manage.py sqlmigrate polls 0001
# Create tables in the db
python manage.py migrate
```

Other Django manage commands:
```bash
# Check for problem with project
python manage.py check
# Open a shell and play around with things like the db API.
python manage.py shell
# Create a Django admin user
python manage.py createsuperuser
```

Python shell testing the DB API:
```python
from polls.models import Choice, Question
Question.objects.all()
from django.utils import timezone
q = Question(question_text="What's new?", pub_date=timezone.now())
q.save()
q.id
q.question_text
q.pub_date
q.question_text = "What's up?"
q.save()
Question.objects.all()

from polls.models import Choice, Question
Question.objects.all()
Question.objects.filter(id=1)
Question.objects.filter(question_text__startswith='What')
from django.utils import timezone
current_year = timezone.now().year
Question.objects.get(pub_date__year=current_year)
Question.objects.get(id=2)
Question.objects.get(pk=1)
q = Question.objects.get(pk=1)
q.was_published_recently()
q = Question.objects.get(pk=1)
q.choice_set.all()
q.choice_set.create(choice_text='Not much', votes=0)
q.choice_set.create(choice_text='The sky', votes=0)
c = q.choice_set.create(choice_text='Just hacking again', votes=0)
c.question
q.choice_set.all()
q.choice_set.count()
Choice.objects.filter(question__pub_date__year=current_year)
c = q.choice_set.filter(choice_text__startswith='Just hacking')
c.delete()
```