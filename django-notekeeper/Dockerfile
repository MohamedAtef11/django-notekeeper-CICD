FROM python:3.8.3-alpine

# set work directory
WORKDIR /usr/src/app
RUN apk add -u zlib-dev jpeg-dev gcc musl-dev 
RUN apk update && apk add --no-cache  libffi-dev g++ build-base linux-headers pcre-dev bash alpine-sdk

RUN python -m pip install --upgrade pip
RUN python -m pip install --upgrade pillow
RUN pip install --upgrade pip 

# install dependencies

COPY ./django-notekeeper/requirements.txt /usr/src/app
RUN pip install -r requirements.txt

# copy project
COPY . /usr/src/app

EXPOSE 8000

RUN python notekeeper/manage.py migrate

CMD ["python", "notekeeper/manage.py", "runserver", "0.0.0.0:8000"]

