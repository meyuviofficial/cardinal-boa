# CARDINAL BOA

This is a codename for the python `Django` Project that I'm developing. This project focusses on developing a `Inventory Management System` as a Service.

## SETUP

Let's look at the setup of this project one by one.

### DJANGO

- Install the Django package using `poetry` or `pip` or `pipenv`

```bash
    python -m pip install django
```

- Once the installation is completed, please try to initiate a project.

```bash
    django-admin startproject [project-name]
```

- You can create multiple apps underneath it.

```bash
    django-admin startapp [app-name]
```

### POSTGRES

- Postgres can be setup easily by running a docker container locally

```bash
 docker run --name postgresql1 -e POSTGRES_PASSWORD=admin123 -p 5432:5432 -d postgres
```

- Once the docker container is running, please try to create a user by logging into the docker container.

```bash
    docker exec -it [docker-hash] bash
```

> Docker hash can be obtained by running `docker container ps`

- Now, once you're inside the docker container, please try to change the password for the user using

```sql
    ALTER USER [username] WITH PASSWORD 'password';
```

> Use psql to login inside the postgresql `psql -h localhost -p 5432 -d postgres -U postgres`

- Now, create a database using the following command.

```sql
    CREATE DATABASE cardinalboa WITH OWNER='postgres';
```

- Now, the `settings.py` should be changed in the django project.

```json
DATABASES = {
    'default': {
        "ENGINE": "django.db.backends.postgresql",
        "NAME": "cardinalboa",
        "USER": "postgres",
        "PASSWORD": "postgres",
        "HOST": "localhost", # change to the ip address of the database server
        "PORT": "5432",
    }
}
```

- Once it's done, please establish a connectivity by running the following command.

```bash
    python ./manage.py migrate
```

> if you're using poetry, please run `poetry run python manage.py migrate`

### TAILWIND CSS

- First install the tailwind css using npm.

```bash
    npm install -D tailwindcss autoprefixer postcss
```

- After that, please initiate the tailwind css using the command `npx tailwindcss init`
- Create a static folder under the root module. Then, create a folder called `src` folder and touch an input file called `input.css` underneath `src` folder
- Add the following contents into the inputs folder

```nodejs
@tailwind base;
@tailwind components;
@tailwind utilities;
```

- Now, install the css sytlesheet by running the following command.

```bash
    npx tailwindcss -i ./static/src/input.css -o ./static/src/styles.css
```

- Also, make the following changes into the tailwind.config.js

```javascript
module.exports = {
  content: ["./users/templates/users/**/*.html"],
  // Add paths to apps that are built in the future
  theme: {
    extend: {},
  },
  plugins: [],
};
```
