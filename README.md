# django-cheatsheet

## django Project Setup

**python3.11 -m venv .venv** - Creates a new virtual environment 

**mkdir django-things** - Creates a new directory for django package 
- Install Django package in django-things with pip install django

**django-admin star project django_things_project .**  

- note: the period above install the project in the current folder

- Does two things:
    1. Creates a folder named django_things_project in the current folder
        * Newly created folder contains starting files
    2. Creates a  “manage.py” file - Django’s command-line utility for admin tasks
        * **python manage.py runserver** - Does 2 things
            1. Starts the development server
                * To exit the server, control + c
        * **python manage.py migrate** - applies all the un-migrated migrations into django

## django App Setup

**python manage.py startapp <app name>** - creates an directory(package) named <app name>
    * MUST connect the app to the project! This is done by going into “settings.py --> add app name to list named “INSTALLED_APPS

## VUT process

V - views.py - handles all of the logic of that call back functionality

	From django.views.generic import TemplateView
	Class HomePageView(Templateview):
	template_name = ‘home.html’

U - urls.py - the file that contains all of the routes to be handles in view.py
	
	from django.urls import path
	from .views import HomePageView

	url patterns = [
		path(‘’, HomePageView.as_view(), name=“home”),
	]

T - templates - directory created in the base “django-things” directory
	 
1. Create a file named “base.html”
    * ! and pressing enter will generate the base html code
    * django tags ({%__some tag__%]) are used in the template files, these serve as a way to connect code in django
   
2. Create a file named “home.html”



## Before Installing Tailwind

1. In order to use tailwind, you must install django compressor
    * $ python -m pip install django-compressor
   
2. Add ‘compressor’ to the installed apps inside the settings.py file

3. Configure the compressor inside the settings.py file with the following code

    ```
    COMPRESS_ROOT = BASE_DIR / 'static'
    COMPRESS_ENABLED = True
    STATICFILES_FINDERS = ('compressor.finders.CompressorFinder’,)
    ```
   
  4. Create two new folders and an input.css file inside the static/src/ folder


## Tailwind CSS

1. Run the following command the install Tailwind CSS as a dev dependency using NPM
    * npm install -D tailwindcss
   
2. Using the Tailwind CLI create a new tailwind.config.js file
    * npx tailwindcss init
   
3. Configure the template paths using the content value inside the Tailwind configuration file

4. Import the Tailwind CSS directives inside the input.css file

    ```
    @tailwind base;
    @tailwind components;
    @tailwind utilities;
    ```

5. Run the following command to watch for changes and compile the Tailwind CSS code
    * npx tailwindcss -i ./static/src/input.css -o ./static/src/output.css --watch

## Installing Flowbite

1. Install Flowbite as a dependency using NPM
    * npm install flowbite
2. Require Flowbite as a plugin inside the tailwind.config.js file
    * require('flowbite/plugin')
3. Include Flowbite inside the content value of the tailwind.config.js file
    * './node_modules/flowbite/**/*.js'
4. Include Flowbite’s JavaScript file inside the _base.html file just before the end of the <body> tag using CDN or by including it directly from the node_modules/ folder
    * <script src="https://cdnjs.cloudflare.com/ajax/libs/flowbite/1.6.5/flowbite.min.js"></script>

## How to check for Django CRUD Completeness

1. Models:
	- Open `snacks/models.py`.
	- Ensure that the `Snack` model has fields like `name`, `description`, `purchaser`, or any other fields mentioned in the assignment.
	- Ensure that the `Snack` model has a `get_absolute_url` method that returns the URL to the snack's detail view. This is useful for redirection after creating or updating a snack.

2. Views:
	- Open `snacks/views.py`.
	- Ensure you have the following class-based views: `SnackListView`, `SnackDetailView`, `SnackCreateView`, `SnackUpdateView`, and `SnackDeleteView`.
	- Each view should be linked to the correct template. For example, `SnackListView` should use a template like `snack_list.html`.
	- Ensure that the `SnackCreateView` and `SnackUpdateView` have the necessary fields defined (e.g., `fields = ['name', 'description', 'purchaser']`).

3. Templates:
	- Check the `snacks/templates/` directory.
	- Ensure you have a `base.html` that provides the basic structure for your site. This should include blocks that other templates can override.
	- Other templates like `snack_list.html`, `snack_detail.html`, `snack_form.html`, and `snack_confirm_delete.html` should extend `base.html` and override the necessary blocks.
	- Ensure forms, links, and display logic are correctly set up in these templates.

4. URLs:
	- Open `snacks/urls.py`.
	- Ensure you have URL patterns for each of your views. They should be correctly mapped to their respective views.
	- Open `snacks_crud_project/urls.py`.
	- Ensure you have included the `snacks/urls.py` using the `include` function.

5. Admin:
	- Open `snacks/admin.py`.
	- Ensure you have registered the `Snack` model for the Django admin using `admin.site.register(Snack)`.

6. Tests:
	- Open `snacks/tests.py`.
	- Ensure you have tests for your models, views, and any other logic. Each test should have a meaningful name and test a specific functionality.
	- You can run the tests using `python manage.py test snacks` to ensure they all pass.

7. Static Files & Media:
	- If your assignment requires static files or media:
		- Ensure `STATIC_URL` and `MEDIA_URL` are set up in `snacks_crud_project/settings.py`.
		- If serving media during development, ensure you've added the necessary URL pattern in `snacks_crud_project/urls.py`.

8. README.md:
	- Open `README.md`.
	- Ensure it has clear instructions on how to set up the project, run it, and test it. Include any prerequisites, installation steps, and how to start the server.

9. Database:
	- In your terminal, run `python manage.py makemigrations` to ensure all model changes are captured in migrations.
	- Run `python manage.py migrate` to apply these migrations and update the database schema.
