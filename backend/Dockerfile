# Use an official Python runtime as a parent image
FROM python:3.10.0-slim-buster

# Set environment variables
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1

# Set the working directory to /myproject
WORKDIR /myproject

# Copy the backend and frontend directories to the container
COPY . /myproject

# Copy the requirements file to the container
COPY ./requirements.txt /myproject/backend/

# Install any needed packages specified in requirements.txt
RUN pip install --no-cache-dir -r backend/requirements.txt

# Run the Django migrations
RUN python ./manage.py migrate

# Install and build the frontend
RUN apt-get update && apt-get install -y curl
RUN curl -sL https://deb.nodesource.com/setup_lts.x | bash -
RUN apt-get install -y nodejs
RUN npm install --prefix /myproject/frontend
RUN npm run build --prefix /myproject/frontend

# Copy the remaining files to the container
COPY . /myproject/
