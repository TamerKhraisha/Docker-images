# Selenium Load testing

Contains a selenium image to perform load testing with.
For each project (website) that you want to test, create a new subfolder and edit the `user_simulation.py` script to your 
needs.

# Usage

## Build docker
First you have to build the container using the script `build_docker.sh <project_name>`. Example:

```
./build_docker.sh usi.datahub.ac
```

The above command will generate an image with tag `load_test_usi.datahub.ac` using the `usi.datahub.ac/user_simulation.py`
 file.

## Generate user folders and credentials
Next you should generate user folders and credentials for storing input credentials data and output screenshots
Make sure you have all the credentails for the different test users in one csv in the format:

```
1,username1,password1
2,username2,password2
...
```

The csv file **must not have** a header line and **must have** an extra empty line at the end.
Once you have the csv, execute `create_credentials.sh <csv_filename>`.
It'll create all the user folders and the required credentials.yaml files.
Example:

```
./create_credentials.sh USI_STAT_2019_Spring_load_test.csv
```

For the purpose of USI testing, there is a Python script called generate_credentials.py which reads a CSV file called 'USI_STAT_2019_Spring_load_test.csv' and generates credentials for users in a txt output format.
> Note that you should not commit user credentials to the repository! For that reason, csv files are addded to gitignore.

## Run the load test
Now you can run the actual load test by executing `start_test.sh <project_name> <start_user_id> <end_user_id>`. Example:

```
start_test.sh usi.datahub.ac 1 100
```

The above command will look for a docker image with tag `load_test_usi.datahub.ac` and will use that image
 to spawn containers `load_test_usi.datahub.ac_*` for users 1-100.

## Checking results

The user folders will contain the output png images, you can check those manually to verify results. 
You can also check the logs of the spawned containers to get some insights.

The `screenshot_statistics.py` script will return a summary statistics of the screenshots and compare them across users using MD5 message-digest algorithm (MD5).
This is a good first estimate to the number of successful runs (there can be false positives). 
screenshot_statistics.py is written in python 3.6, so to run it you might need to do :

```
python3.6 screenshot_statistics.py
```

## Cleaning up

Make sure you clean up the unused docker containers regularly with the command `docker container prune`.

It is possible to remove all containers running for a specific image by running `remove_containers.sh`, e.g. to remove containers launched to test 50 users using the image load_test_draps.alphacruncher.net, you can do:

```
bash remove_containers.sh draps.alphacruncher.net 1 50
```



You can delete all `png` files from the user folders using `delete_screenshots.sh`.
