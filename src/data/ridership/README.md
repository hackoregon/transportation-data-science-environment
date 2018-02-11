# Creating the Ridership database / backup

## Setup
1. Clone this repo.
2. `cd transportation-data-science-environment`.
3. Create and activate a Python or Conda virtual environment and type `pip -r requirements.txt`.
4. Configure your AWS S3 access.
5. `cd transportation-data-science-environment/src/data-science-pet-containers/containers`.
6. `docker-compose build` to make the Docker images. This takes some time; it creates about 5.3 gigabytes of Docker images.

You only need to do the above steps once.

## Execution
1. Activate your virtual environment.
2. `cd transportation-data-science-environment; make sync_data_from_s3`.
3. `cd transportation-data-science-environment/src/data/ridership`.
4. Create the file `.env`. Define the variables `HOST_PORT` and `POSTGRES_PASSWORD`.
5. `./run.bat`.
6. `cd transportation-data-science-environment; make sync_data_to_s3`.
