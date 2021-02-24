# tutorial of docker-compose

## explanation of Dockerfile

```
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

- ```FROM``` indicates building the image with the ```python:3.7-alpine``` image.
- ```WORKDIR``` will set working directory to ```/code``` directory. for more, read ```https://www.educative.io/edpresso/what-is-the-workdir-command-in-docker```.
- ```ENV``` indicates the environment variables which are going to be used by flask command.
- ```RUN``` helps you to run commands. for more, read ```https://nickjanetakis.com/blog/docker-tip-7-the-difference-between-run-and-cmd```
- ```EXPOSE ``` It is the instruction informs Docker that the container listens on the specified network ports at runtime. You can specify whether the port listens on TCP or UDP, and the default is TCP if the protocol is not specified. resource ```https://docs.docker.com/engine/reference/builder/#expose```
- ```COPY``` The COPY instruction copies new files or directories from ```<src>``` and adds them to the filesystem of the container at the path ```<dest>```. resource ```https://docs.docker.com/engine/reference/builder/#copy```. For example ```COPY . .``` copies the current directory ```.``` in the project to the workdir ```.``` in the image.
- ```CMD``` sets the default command for the container to ```flask run```. for more info, ```https://docs.docker.com/engine/reference/builder/#cmd```

## explanation of YAML file ```docker-compose.yml```

```
version: "3.9"
services: 
  web:
    build: . 
    ports: 
      - "5000:5000"

  redis:
    image: "redis:alpine"
```

- SOON


## resources

- for more concrete knowledge of redis, read ```https://realpython.com/python-redis/```
- ```https://en.wikipedia.org/wiki/Flask_(web_framework)```
- ```https://docs.docker.com/compose/gettingstarted/```
- for understanding app routing on app.py, ```https://www.javatpoint.com/flask-app-routing``` 
- ```https://docs.docker.com/engine/reference/builder/#expose```