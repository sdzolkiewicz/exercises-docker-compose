## Solution

### Background

Alongside this course, I have been practicing Spring Boot, so I decided to set up development containers using `docker-compose.yaml` and Dockerfiles for my personal training project.

The project is a Trello clone for project management. It is a monorepo with a React frontend and a Spring Boot backend.

### Steps

- Created Dockerfiles for both apps in monorepo:
  - `frontend`, based on the `node:24-alpine` image,
  - `backend`, based on the `maven:3.10.0-amazoncorretto-25` image.
- Added a `docker-compose.yaml` in the project root that defines `frontend` and `backend`. For each it:
  - maps the ports to the host,
  - bind mounts the source code into the container,
  - starts the app in dev mode using `command:`.
- Added named volumes:
    - `node_modules` like in this course to protect node_modules from being overwritten by the bind mount,
    - Maven `.m2` cache, so dependencies are not downloaded again on every start.

### Results

- The whole project starts with a single command: `docker compose up`.
- The frontend and backend work together: the app running in the browser sends requests to the backend on its mapped port and gets valid response.
- Code changes are picked up instantly:
  - **Frontend:** changes are visible in the browser.
  - **Backend:** after a code change, the container logs show that the app reloaded. For example, when I changed the payload returned by a Spring controller, the frontend received the updated data.

### Future work

- As the backend grows, I plan to update `docker-compose.yaml`:
    - add PostgreSQL, store the db in named volume,
    - add Adminer for managing the database in browser.