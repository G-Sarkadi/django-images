# django-images

A simple image hosting application written in Django.

This is a clone of the following project: https://github.com/duplxey/django-images  
The project is used as a demo application for practice deployment to Azure. The Terraform code for the deployment can be found here: https://github.com/G-Sarkadi/django-infra. I've mostly followed this tutorial for setup the deployment: https://testdriven.io/blog/django-azure-app-service/  
My changes from the original repository:
- The debug status, secret key, allowed hosts and secure ssl redirection setups are now set by environment variables (settings.py)
- The database is changed from SQlite to PostgreSQL, the database host, name, username and password also comes from environment variables (also settings.py)
- The server is changed from Django's development server to Gunicorn
- Static and media files are stored in an Azure blob storage, the details for this also set by env variables (settings.py)
- These two blob storage need two new classes, those are defined in a new 'azure_storage.py' file.

## Want to use this project?

1. Fork/Clone

2. Create and activate a virtual environment:

    ```sh
    $ python3 -m venv venv && source venv/bin/activate
    ```

3. Install the requirements:

    ```sh
    (venv)$ pip install -r requirements.txt
    ```
4. Create a .env file, leave it out from version control, set up the necessary environmental variables:
    ```sh
    SECRET_KEY = "django-app-unsafe-key"
    DEBUG = "debug-status-0-or-1"
    ALLOWED_HOSTS = "list-of-allowed-hosts"
    CSRF_TRUSTED_ORIGINS = "list-of-trusted-origins"
    SECURE_SSL_REDIRECT = "ssl-redirection-status-0-or-1"
    DBNAME = "postgresql-db-name"
    DBHOST = "postgresql-db-host"
    DBUSER = "postgresql-db-username"
    DBPASS = "postgresql-db-unsafe-password"
    AZURE_ACCOUNT_NAME = "azure-storage-account-name"
    AZURE_ACCOUNT_KEY = "azure-storage-account-primary-key"
    ```

5. Apply the migrations:

    ```sh
    (venv)$ python manage.py migrate
    ```

6. Run the server:

    ```sh
    (venv)$ python manage.py runserver
    ```
    
 7. Navigate to the url of the running application in your favorite web browser.  
 Check out the linked tutorial or the infrastructure repo for details.