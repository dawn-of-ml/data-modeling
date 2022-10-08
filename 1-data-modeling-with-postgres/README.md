## Data Modeling with Postgres

A startup called Sparkify wants to analyze the data they've been collecting on songs and user activity on their new music streaming app.
The analytics team is particularly interested in understanding what songs users are listening to. Currently, they don't have an easy
 way to query their data, which resides in a directory of JSON logs on user activity on the app, as well as a directory with JSON 
 metadata on the songs in their app.

- Create a database schema
- Create ETL pipeline
- Test your database and ETL pipeline
### Datasets available

The song dataset is a subset of real data from the [Million Song Dataset](https://labrosa.ee.columbia.edu/millionsong/). Each file is in JSON format and contains metadata about a song and the artist of that song. The files are partitioned by the first three letters of each song's track ID.

The log dataset consists of log files in JSON format generated by [this event simulator](https://github.com/Interana/eventsim) based on the songs in the dataset above. These simulate activity logs from a music streaming app based on specified configurations.

### Setup Instructions and Steps followed
* setup a local postgres database as [explained](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-postgresql-on-ubuntu-20-04)
```bash
chmod u+x setup_postgressql.sh setup_env.sh
bash setup_postgressql.sh #enter your username and password before running
bash setup_env.sh
```
* create a default database, username and password
`
sudo -i -u postgres #switching Over to the postgres Account
createdb sepideh
createuser --interactive #Creating a new user
psql #access postgres prompt
\password <username> #setup password
\q #quit
`
### Setup virtual environment
`
sudo apt-get install python3.8-dev
virtualenv -p python3.8 ./venv3.8
source ./venv3.8/bin/activate
./venv3.8/bin/pip3 install -r requirements.txt
./venv3.8/bin/pip3 install jupyterlab
`
### Program execution

* Execute the script to generate the database and its tables by executing `python3 create_tables.py`.
* Load the data and insert it to the database by executing `python3 etl.py`.

### Schema Design

* The fact table `songplays` stores the records in log data associated with song plays i.e. records with page.
* The dimension table `users` stores the users in the app.
* The dimension table `song` stores the songs in the music database.
* The dimension table `artists` stores the artists the in music database.
* The dimension table `time` stores the timestamps of records in songplays broken down into specific units.

### Purpose of this database

This database allows to aggregate all songs, artists, users and songplays in a single database. In this way, the company disposes of the needed data stored in a unique structure and can thus analyze different scenarios easily. For instance, one can analyze the popularity of different songs or artists. Also, it is possible to perform analysis with geographic information. One can for instance determine which song is popular in which country and region.