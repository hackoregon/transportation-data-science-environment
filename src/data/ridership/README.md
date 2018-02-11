# Creating the Ridership database / backup

## Setup
1. You'll need `conda`.
2. Clone this repo. `git clone --recurse-submodules git@github.com:hackoregon/transportation-data-science-environment`.
3. `cd transportation-data-science-environment`.
4. `make create_environment`. This will create a Conda environment named `transportation-data-science-environment`.
5. `source activate transportation-data-science-environment`.
6. `make requirements`.
7. Configure your AWS S3 access. Place the `passenger_census.csv` file in `transportation-data-science-environment/data/raw/`. 
8. Set the environment variables BUCKET and PROFILE to your AWS S3 bucket and profile names. Then `cd transportation-data-science-environment; make sync_data_to_s3`.
9. `cd transportation-data-science-environment/src/data-science-pet-containers/containers`.
10. `docker-compose build` to make the Docker images. This takes some time; it creates about 5.3 gigabytes of Docker images.

You only need to do the above steps once.

## Execution
1. Activate your virtual environment.
2. `cd transportation-data-science-environment; make sync_data_from_s3`.
3. `cd transportation-data-science-environment/src/data/ridership`.
4. Create the file `.env`. Define the variables `HOST_PORT` and `POSTGRES_PASSWORD`. Docker will map the container port 5432 onto the HOST_PORT on `localhost`.
5. `./run.bat`. The `passenger_census` service will start up, load the data into a database and create a backup file. When the database announces it is ready to accept connections, type `CTRL-C`.
6. `run.bat` will copy the database backup from the container - `ridership_passenger_census_1:/interim/passenger_census.backup` - to `transportation-data-science-environment/data/interim/`.
6. `cd transportation-data-science-environment; make sync_data_to_s3`.

## Using the service
When you typed `CTRL-C` above, Docker stopped the `ridership_passenger_census_1` container so `run.bat` could copy the backup file out. But the container is still there, and its filesystem has the database loaded! Just type `docker-compose up -d` and Docker will restart the `ridership_passenger_census_1` container with the `passenger_census` service. You can connect to the service as `postgres` with password POSTGRES_PASSWORD on `localhost`, port HOST_PORT.
