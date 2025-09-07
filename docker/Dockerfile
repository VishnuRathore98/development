# All custom images starts with a base image
# FROM <image>:<version>
FROM python:3.9.7

# Setting the working directory
# This will be our present working directory inside which all of our work will be saved
WORKDIR /usr/src/app

# Copy requirements.txt from our local to container's WORKDIR which is our current working
# directory which we mentioned earlier or else we had to give the full path to our
# working directory
COPY requirements.txt ./

# Run the pip command to install the dependencies
RUN pip install --no-cache-dir -r requirements.txt

# Now we will copy everything from our local working dir to our container's working dir
# all of our source code.
COPY . .

# In docker when we build images from dockerfiles it runs each of these commands one by one 
# in a layer, so copying all the content after installing requirements.txt is a optimization
# technique. 
# When building the images it caches the results at each step or layer, it is important as 
# when we caches the results and if nothing changes, then we can just use the chached results.
# Each layer has its cached results so if we have just changed some logic in code we dont have 
# to rerun the pip installing as it is a time consuming and resource consuming task.
# If something changes in requirements.txt then it will execute COPY -> RUN -> COPY, that means
# anything changes at any layer then all the steps including that layer and the subsequent layers
# will execute again.

# Now we will run the commands that we want to run inside our docker container once it is initialized
# each command seperated by a space that is written inside a seperate quotes in the CMS list.
CMD ["uvicorn","app.main:app", "--host", "0.0.0.0", "--port", "8000"]

# Running the docker build command, this will build the docker image from this dockerfile:
# > docker build -t <image-tag> <path-to-dockerfile> 
# > docker build -t app_backend .

# To check all the available images:
# > docker image ls

# Let's use docker-compose to run and configure out docker commands.
