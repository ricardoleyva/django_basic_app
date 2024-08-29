Creating a Django App
	Initialization
		Create an app project
	Core development
		Testing
		Build UI
		MAP URLs --> urls.py
		Create views --> views.py (functions and classes)
		Create models --> models.py (also migrations folder contains DB scripts)
	Add-ons
		Admin site --> admin.py
		Security
		3rth party frontend
		Configuration --> apps.py
		Localization
		Logging
	Deployment and monitoring
		Performance
		Packaging and deployment

STEPS FOR CREATING DJANGO APP
Step 1:
	Initialization of project
		pip install --upgrade distro-info
		pip3 install --upgrade pip==23.2.1
		pip install virtualenv
		virtualenv djangoenv
		djangoenv/Scripts/activate.ps1 (Linux would be source djangoenv/bin/activate)
	Install Django:
		pip install Django
	Create Django project:
		django-admin startproject mysite
		Creates structure:
		mysite/
			manage.py
			mysite/
				__init__.python
				settings.py
				urls.py
				...
Step 2:
	Run start app command: 
	$python manage.py startapp onlinecourse
		onlinecourse/
			__init__.py
			admin.py
			models.py
			views.py
			urls.py
			apps.py
			migrations/
Step 3:
	Include Django app to project
		Open mysite/settings.py
		Find INSTALLED_APPS setting, add:
		INSTALLED_APPS = [
			'onlinecourse.apps.OnlinecourseConfig'
			...
			]

Step 3.1 (optional):
	Setup database
		Open mysite/settings.py
		Find DATABASES setting, add:
		DATABASES = {
			'default':{
				'ENGINE':'django.db.backends.sqlite3'
				'NAME': DB_DIR / 'db.sqlite3'
			}
		}

Step 4:
	Define models and create migration scripts
		Example:
		1. Create model 
		class Course(Models.model):
			name = models.CharField(max_lenght=30)
			description = models.CharField(max_lenght=500)
		2. Create migration scripts
		python manage.py makemigrations onlinecourse
		3. Check generated SQL (this shows translation from object CLASS in PYTHON to TABLE in SQL)
		pyton manage.py sqlmigrate onlinecourse 001
		4. Run migrations
		python manage.py migrate
Step 5:
	Create a simple view and template
		Open onlinecourse/views.py and add:
		from django.http import HttpResponse
		from .models import Course

		def table_example_list(request):
			table_example = Course.objects.get(pk=1)
			template = "<html>"\
				"<body>The first table example we created is `%s.`"\
				"</body>"
				</html> % course.name
			return HttpResponse(content=template)
		...
Step 6:
	Configure view URL
		Create urls.py under onlinecourse/ and add urlpatterns list:
			from django.urls import path
			from . import views
			urlpatterns = [
				path(route='', view=views.table_example_list, name='table_example')
			]
			...
		Include online course urls.py to mysite/urls.py:
			from django.contrib import admin
			from django.urls import include, path
			urlpatterns = [
				path('admin/', admin.site.urls),
				path('onlinecourse/', include('onlinecourse.urls')),
			]
			...
Step 7:
	Run the app (default host is localhost oe 127.0.0.1 at port 8000)
		python manage.py runserver
		Go to: http://127.0.0.1:8000/onlinecourse/ and check the first Web page rendered


		
