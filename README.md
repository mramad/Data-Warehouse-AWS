# Data-Warehouse-AWS
Cloud DataWarehouse | Python | AWS

This Project sets the ground for a startup called "Sparkify" to analyze their data. Specifically user activity log data and songs metadata are processed into a cloud warehouse database in order to create a star schema data model which can be used by "Sparkify" analytics team in order to analyze thier customers behaviours.

For this purpose, this project does the following:

- Connects to a cloud warehouse database (Amazon Redshift)
- Create data staging tables which are used to stage User activity data along with song metdata which are stored in Amazon S3
- Model a datawarehouse star schema which will be used to analyze the loaded users/songs data using relational modeling.
- Dimensions are created to represent the metadata (songs,artists,Users and Time)
- Single Fact table (songplays) is created to insert the user activity data
- Referental integrity constraints are added where applicable
- Uses Python ETL Pipelines in order to:
   - Loads staging data from Amazon S3 into the cloud datawarehouse 
   - Insert data into desired dimension & fact tables
  
Project Datasets:
 
- These datasets is loaded into Amazon S3 Bucket, during etl process, the scripts load the data from S3 into RDS staging tables

- Song Dataset: This is a JSON format metadata about a song and the artist of that song. 
- Log Dataset: This is a JSON format user activity log data 

Data Transformation:

- First the data will be loaded "AS IS" from S3 into RDS staging tables
- Then the data will be transformed into a star schema datawarehouse design as the following:
     - User Diemnsion: Hosts unique User data (using Userid); this was loaded and transformed from the log dataset (Staging_events)
     - Song Dimension: Hosts unique Song data ( using songid); this was loaded and transformed from the song dataset (Staging_songs) 
     - Artist Dimension: Hosts unique artist data (using artistid); this was loaded and transformed from the song dataset (Staging_songs) 
     - Time Dimension: Hosts unique time data (using ts); this was loaded and transformed from the log dataset (Staging_events) ; ts integer format was        transformed into timestamp format and date parts such as year, month, day and hour details were extracted out of the timestamp format
     - Songplays Fact table: Hosts fact data about user activity log data that was extracted from both log and song data sets; data was filtered to            select only "song play (NextSong)" actions and minor data casting was performed in order to accommodate the fact table data types.

Data Analytics:

- Data Analysis exercises can be performed on the datawarehouse schema in order to analyze users behaviour, since data is cleansed and loaded into fact and dimension tables as explanied above; the following statistics can be obtained from the datawarehouse schema:

    - Number of songplays activities done in a certain timeframe grouped by a specific song, artist, level,location or a useragent or any combination         of these.
    

The Project has four files detailed as the following:

create_tables.py: This file drops the staging and star schema tables if they exist and create fresh ones.

etl.py: This file does the following:

    - loads user activity and songs data from S3 into the staging tables.
    - process the data from the staging tables into the star schema tables. 

sql_queries.py: has the sql queries to drop,create and insert data into datawarehouse tables, it has also scripts to load the data from S3 into datawarehouse staging tables.

dwh.cfg: This file has the AWS cloud configuration data as the following:
    -config data for AWS access (This has been removed for secuitry purposes)
    -cluster access details
    -IAM role details
    -S3 Access details

Project Run:

In order to run the project, please follow the below sequence.

- Run create_tables.py, this should connects to the cloud datawarehouse, drops tables if they exist and create fresh ones.

- Run etl.py, this should then process the data from S3 into staging tables and then into star schema datawarehose tables.

