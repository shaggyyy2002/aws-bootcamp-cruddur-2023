# Base Image for Python:version
FROM python:3.10-slim-buster

# This will create our workdir and cd into it
WORKDIR /backend-flask

# Copies our file from our source to destination path
COPY requirements.txt requirements.txt

# The RUN instruction will execute any commands in a new layer on top of the current image and commit the results
RUN pip3 install -r requirements.txt

COPY . .

# The ENV instruction sets the environment variable <key> to the value <value>. 
# This value will be in the environment for all subsequent instructions in the build stage and can be replaced inline in many as well.
ENV FLASK_ENV=development

EXPOSE ${PORT}

# CMD (Command)
# python3 -m flask run --host=0.0.0.0 --port=4567
CMD [ "python3", "-m" , "flask", "run", "--host=0.0.0.0", "--port=4567"]