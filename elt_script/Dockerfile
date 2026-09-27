#This file allows you to build one specific container

FROM python:3.8-slim 
# start an official python 3.8 image (slim = smaller version with only essentials)


RUN apt-get update && apt-get install -y postgresql-client-15
# Install PostgreSQL command-line tools and run this while building the image

# Copy the ELT script 
COPY elt_script.py .

# Set the default command to run the ELT script
CMD ["python", "elt_script.py"]