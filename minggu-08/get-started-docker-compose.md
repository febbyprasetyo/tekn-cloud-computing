# Try Docker Compose

## Prerequisites

You need to have Docker Engine and Docker Compose on your machine. You can either:

- Install [Docker Engine](https://docs.docker.com/get-docker/) and [Docker Compose](https://docs.docker.com/compose/install/) as standalone binaries

- Install [Docker Desktop](https://docs.docker.com/desktop/) which includes both Docker Engine and Docker Compose

You don’t need to install Python or Redis, as both are provided by Docker images.

## Step 1: Define the application dependencies🔗

1. Create a directory for the project:

![1](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/87804be0-7211-4e4a-8c53-2f380e7fd041)

2. Create a file called app.py in your project directory and paste the following code in:

```
import time

import redis
from flask import Flask

app = Flask(__name__)
cache = redis.Redis(host='redis', port=6379)

def get_hit_count():
    retries = 5
    while True:
        try:
            return cache.incr('hits')
        except redis.exceptions.ConnectionError as exc:
            if retries == 0:
                raise exc
            retries -= 1
            time.sleep(0.5)

@app.route('/')
def hello():
    count = get_hit_count()
    return 'Hello World! I have been seen {} times.\n'.format(count)
```

3. Create another file called ``requirements.txt`` in your project directory and paste the following code in:

```
flask
redis
```

## Step 2: Create a Dockerfile

The Dockerfile is used to build a Docker image. The image contains all the dependencies the Python application requires, including Python itself.

1. In your project directory, create a file named Dockerfile. Code

```
# syntax=docker/dockerfile:1
FROM python:3.7-alpine
WORKDIR /code
ENV FLASK_APP=app.py
ENV FLASK_RUN_HOST=0.0.0.0
RUN apk add --no-cache gcc musl-dev linux-headers
COPY requirements.txt requirements.txt
RUN pip install -r requirements.txt
EXPOSE 5000
COPY . .
CMD ["flask", "run"]
```

## Step 3: Define services in a Compose file

1. Create a file called ```docker-compose.yml``` in your project directory and paste the following code in:

```
services:
  web:
    build: .
    ports:
      - "8000:5000"
  redis:
    image: "redis:alpine"
```

2. Finally, the files in your project directory will be like this

![2](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/c4ab5e93-2ce9-43f3-adab-ac29ac184853)

## Step 4: Build and run your app with Compose

1. From your project directory, start up your application by running ```docker compose up.```

![3](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/cc8e3040-f9ce-4124-ad61-854e03317f03)

![4](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/f1c78e7b-79b5-4d2b-bcab-e8d1589097b7)

2. Enter http://localhost:8000/ in a browser to see the application running.

You should see a message in your browser saying:

```
Hello World! I have been seen 1 times.
```

![5](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/b9591374-ba47-4562-8381-09112d195e8a)

3. Refresh the page. The number should increment.

![6](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/cd7ce412-662c-4de3-9a2a-67f77647a047)

4. Switch to another terminal window, and type ```docker image ls``` to list local images.

Listing images at this point should return redis and web.

![7](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/ad7e3e09-346f-4546-b27c-a87306db2777)

5. Stop the application, either by running ``docker compose down`` from within your project directory in the second terminal, or by hitting CTRL+C in the original terminal where you started the app.

![8](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/4f0d1a6b-25b5-4a52-bf59-8805eee6bcbb)

## Step 5: Edit the Compose file to add a bind mount

1. Edit ``docker-compose.yml`` in your project directory to add a bind mount for the web service:

```
services:
  web:
    build: .
    ports:
      - "8000:5000"
    volumes:
      - .:/code
    environment:
      FLASK_DEBUG: "true"
  redis:
    image: "redis:alpine"
```

## Step 6: Re-build and run the app with Compose

1. From your project directory, type docker compose up to build the app with the updated Compose file, and run it.

![13](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/1a2dbedf-0c4c-466a-a39e-7b9ffce516c8)

2. Check the Hello World message in a web browser again, and refresh to see the count increment.

![14](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/f175f618-6e47-4a94-8fb7-b0d926f89ff7)

## Step 7: Update the application

Because the application code is now mounted into the container using a volume, you can make changes to its code and see the changes instantly, without having to rebuild the image.

Change the greeting in app.py and save it. For example, change the Hello World! message to Hello from Docker!:

```
return 'Hello from Docker! I have been seen {} times.\n'.format(count)
```

Refresh the app in your browser. The greeting should be updated, and the counter should still be incrementing.

![15](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/2c85577d-83cd-4e01-ab1d-2550824fa7dc)

## Step 8: Experiment with some other commands

1. If you want to run your services in the background, you can pass the -d flag (for “detached” mode) to ``docker compose up`` and use ``docker compose ps`` to see what is currently running:

![16](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/6794d40b-01b5-486e-9ed2-59b131ac7e52)

2. The ``docker compose run`` command allows you to run one-off commands for your services. For example, to see what environment variables are available to the web service:

![17](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/faa6da11-e44d-401d-a3b2-f8d49b235a4e)

3. If you started Compose with docker ``compose up -d,`` stop your services once you’ve finished with them:

![18](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/c9baa4a8-0ee3-4ee5-b3c3-061ed74de8eb)

4. You can bring everything down, removing the containers entirely, with the down command. Pass --volumes to also remove the data volume used by the Redis container:

![19](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/5cc07bb4-e864-48f7-87f2-4591be6d8221)







