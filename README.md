# Setup

1. Ensure steps in [frontend setup](./frontend/README.md) are complete as the frontend dev server gets run locally

2. [app server python setup](./web/README.md) is optional, though pyenv and poetry are nice to have locally for other stuff

3. Bring up backend dev build

```
docker compose up -d --build
```

4. In vs code, ensure remote development extension pack is installed

5. Open up ./web directory in a vs code window

6. cnrl+p to open up command pallet and click `Remote-Containers: Open Folder in Container`

7. This hijacks the entry point in the web container so start the django server by running:```
python manage.py runserver 0.0.0.0:8000``` in the vs code terminal of the window attached to the container

8. Now making changes to the django code should update the running app

9. frontend located at http://localhost:5173/

10. backend located at http://localhost:8000/

11. If things ever get proper buggered just run `docker compose down -v` and restart from step 3
