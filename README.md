# Project Overview: Introduction to NoSQL Databases

## Scenario
You are a data engineer at a Data Analytics Consulting Company. Your company prides itself in being able to efficiently handle data in any format on any database on any platform. Analysts in the offices need to work with data on different databases, and with data in different formats. While they are good at analyzing data, they count on you to be able to move data from external sources into various databases, move data from one type of database to another, and be able to run basic queries on various databases.

## Check the lab environment:
- You need the ‘couchimport’ and ‘couchexport’ tools to move data in and out of the Cloudant database.
>> ![install-couchimport](./Images/0.install-couchimport1.png)\
>> ![install-couchimport](./Images/1.install-mongoexport.png)

- You need to obtain the content of the json file and copy the entire content: [movies.json](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DB0151EN-SkillsNetwork/labs/Final%20Assignment/data/movie.json)

- Create a new file named movie.json under the project directory and paste the entire content copied earlier into the newly created json file.

- Go to your Cloudant Service created on IBM Cloud and then click on Launch Dashboard to launch the cloudant databases. Then, click on New database on the top-right corner and create a Non-patitioned database named movies.

> 1. Log in to IBM Cloud
>>> - You need an IBM Cloud account to work with IBM Cloudant.
>>>- If you do not have an account, you can sign up for one using the instructions [here](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-CC0100EN-SkillsNetwork/labs/IBMCloud_accountCreation/CreateIBMCloudAccount.md.html).
>>>>> Step 1: Navigate to [cloud.ibm.com](https://cloud.ibm.com/?utm_medium=Exinfluencer&utm_source=Exinfluencer&utm_content=000026UJ&utm_term=10006555&utm_id=NA-SkillsNetwork-Channel-SkillsNetworkCoursesIBMDB0151ENSkillsNetwork884-2022-01-01). \
>>>>> Step 2: Login using your IBM cloud credentials. \
>>>> You will land on the the Cloud Dashboard page.

> 2. Create an IBM Cloudant instance
>>> Step 1: Click on [cloud.ibm.com/catalog/services/cloudant](https://cloud.ibm.com/catalog/services/cloudant?utm_medium=Exinfluencer&utm_source=Exinfluencer&utm_content=000026UJ&utm_term=10006555&utm_id=NA-SkillsNetwork-Channel-SkillsNetworkCoursesIBMDB0151ENSkillsNetwork884-2022-01-01) to create a Cloudant instance. \
>>> Or you can alternatively click on <span style="color:orange">Create Resource</span>, search for Cloudant on the Dashboard page. \
You will be taken to the Cloudant instance creation page.
![cloudant-create-instance](./Images/cloudant-create-instance.png) \
Step 2: Select the region under the “Available regions”. \
It is OK to go with the default option, if you cannot figure out which region to choose.\
Step 3: Scroll down to configure Cloudant instance.
![cloudant-create-instance-steps](./Images/cloudant-create-instance-steps.png)
Step 4: Set your instance name to <span style="color:orange">mycloudant</span> or anything else that you prefer.\
Step 5: Authentication Method is a critical setting. Select “IAM and legacy Credentials” as your Authentication Method. If you choose any other Authentication Method, some labs will not work.
Step 6: Select the Lite plan. \
Step 7: Click on <span style="color:orange">Create</span> \
You should see a screen like this
![cloudant-instance-create2](./Images/cloudant-instance-create2.png)\
Your Cloudant service will be created and you will be redirected to the Resource list page. \
Step 8: If you are not redirected, you can click on this link [cloud.ibm.com/resources?groups=resource-instance](https://cloud.ibm.com/resources?utm_medium=Exinfluencer&utm_source=Exinfluencer&utm_content=000026UJ&utm_term=10006555&utm_id=NA-SkillsNetwork-Channel-SkillsNetworkCoursesIBMDB0151ENSkillsNetwork884-2022-01-01&groups=resource-instance) \
You may see a screen like this, indicating the Provision in progress.
![cloudant-instance-create3](./Images/cloudant-instance-create3.png)
Step 9: Wait till the status turns ‘Active’ and click on <span style="color:orange">mycloudant</span>  or your custom instance name.
![cloudant-instance-create4](./Images/cloudant-instance-create4.png)\
You will be taken to the Cloudant instance page. \
You have successfully created the Cloudant instance.

> 3. Create Cloudant Service credentials
>>> Step 1: On the Cloudant instance page, click on <span style="color:orange">Service Credentials</span>
![cloudant-instance-page](./Images/cloudant-instance-page.png)\
Step 2: Click on <span style="color:orange">New Credential</span>.
![create-credentials1](./Images/create-credentials1.png)\
Step 3: Create credential pop up appears. Accept the default values for Name and Role and click on <span style="color:orange">Add</span>
![create-credentials2](./Images/create-credentials2.png)\
Step 4: Your Cloudant Service credentials will be created. Click on the chevron to view the credentials. \
DO NOT attempt to use the credentials shown here. These are expired credentials.
![create-credentials3](./Images/create-credentials3.png)\
Step 5: You will be using the username, password and url in the next labs.
![create-credentials4](./Images/create-credentials4.png)\
You have successfully created a Cloudant instance and Service credentials for your instance.

>> Note: If you do not see the password field in your credentials, it is because you have not selected “IAM and legacy credentials”. You can fix it by deleting your current Cloudant instance and following this lab from the beginning to create a new instance of Cloudant.

- Export the json into your Cloudant Database:
>> Go to your Cloudant Service created on IBM Cloud and then click on Launch Dashboard to launch the cloudant databases. Then, click on New database on the top-right corner and create a Non-patitioned database named movies.
![create-database-movies](./Images/create-database-movies.png)\
>> Export the data of the “movie.json” file into your Cloudant database “movies”:

>> export CLOUDANTURL="https://apikey-v2-33nzi87wa2cxaku7ymd2qo7mpww3tr44fwb8eclw8vb5:6832de0422bffee7c2c833cb911d9444@69e7b6d9-df64-418d-9363-5536084686fd-bluemix.cloudantnosqldb.appdomain.cloud"

![export-CloudantURL](./Images/export-CloudantURL.png)\
<span style="color:orange">curl -XPOST $CLOUDANTURL/movies/_bulk_docs -Hcontent-type:application/json -d @movie.json</span>

>>![export-Into-CloudantURL](./Images/export-Into-CloudantURL.png)

## Task 1 - Replicate a local database into your Cloudant instance
>> ![Replicate](./Images/Replicate-a-local-database-into-yourCloudant-instance1.png)\
![Replicate](./Images/Replicate-a-local-database-into-yourCloudant-instance2.png)
![Replicate](./Images/Replicate-a-local-database-into-yourCloudant-instance3.png)

## Task 2 - Create an index for the “Director” key, on the ‘movies’ database using the HTTP API
>> ![Task2](./Images/Create-Index-Director.png)

## Task 3 - Write a query to find all movies directed by ‘Richard Gage’ using the HTTP API
>> ![Task3](./Images/3-query-director.png)

## Task 4 - Create an index for the “title” key, on the ‘movies’ database using the HTTP API
>> ![Task4](./Images/4-index-title.png)

## Task 5 - Write a query to list only the “year” and “Director” keys for the ‘Top Dog’ movies using the HTTP API
>> ![Task5](./Images/5-query-title.png)

## Task 6 - Export the data from the ‘movies’ database into a file named ‘movies.json’
>> npm install -g couchimport@1.4.0 \
>> couchexport --url $CLOUDANTURL --db movies --type jsonl > movies.json

>> ![Task6](./6-couchexport.png)

## Task 7 - Import ‘movies.json’ into mongodb server into a database named ‘entertainment’ and a collection named ‘movies’

- You need the ‘mongoimport’ and ‘mongoexport’ tools to move data in and out of the mongodb database. To install these tools run the below commands on the terminal.
- >> wget https://fastdl.mongodb.org/tools/db/mongodb-database-tools-ubuntu1804-x86_64-100.3.1.tgz
tar -xf mongodb-database-tools-ubuntu1804-x86_64-100.3.1.tgz
export PATH=$PATH:/home/project/mongodb-database-tools-ubuntu1804-x86_64-100.3.1/bin
echo "done"

Start the mongodb server:
>>> <span style="color:orange">start_mongo</span> 

Make a note of the username and password based on the output of the previous command.\
Import data in ‘movies.json’ into a collection named ‘entertainment’ and a database named ‘movies’, replacing the password (the characters following -p: <span style="color:orange">NjEwOC1haG1lZGFi</span>) with your own password.
>>> <span style="color:orange">mongo -u root -p NjEwOC1haG1lZGFi --authenticationDatabase admin local</span>

Create database and collection
>>> ![Create-db-document-Mongodb](./Images/Create-db-document-Mongodb.png)

Import ‘movies.json’ into mongodb server
>> mongoimport -u root -p NjEwOC1haG1lZGFi --authenticationDatabase admin --db entertainment --collection movies --file movies.json

>>> ![mongoimport](./Images/7-mongoimport.png)

## Task 8 - Write a mongodb query to find the year in which most number of movies were released
>> db.movies.aggregate([{"$group":{"_id":"$year","moviecount":{"$sum":1}}},{"$sort":{"moviecount":-1}}])

>> db.movies.aggregate([{"$group":{"_id":"$year","moviecount":{"$sum":1}}},{"$sort":{"moviecount":-1}},{"$limit":1}])

>>> ![The year in which most number of movies were released](./Images/8-mongo-query.png)

## Task 9 - Write a mongodb query to find the count of movies released after the year 1999
>> db.movies.find({"year":{"$gt":1999}}).count()

>>> ![The count of movies released after the year 1999](./Images/9-mongo-query.png)

## Task 10. Write a query to find out the average votes for movies released in 2007
>> db.movies.aggregate([{"$match":{"year":2007}},{"$group":{"_id":"$year", "average":{"$avg":"$Votes"}}}])

>>> ![The average votes for movies released in 2007](./Images/10-mongo-query.jpg)

## Task 11 - Export the fields _id, “title”, “year”, “rating” and “director” from the ‘movies’ collection into a file named partial_data.csv

>> mongoexport -u root -p NjEwOC1haG1lZGFi --authenticationDatabase admin --db entertainment --collection movies --out partial_data.csv --type=csv --fields _id,Director,rating,title,year

>>> ![Export the fields from mongodb](./Images/11-mongoexport.jpg)

## Task 12 - Import ‘partial_data.csv’ into cassandra server into a keyspace named ‘entertainment’ and a table named ‘movies’

>> start_cassandra

>> cqlsh --username cassandra --password MTIxMTMtYWhtZWRh

>> CREATE KEYSPACE entertainment  
WITH replication = {'class':'SimpleStrategy', 'replication_factor' : 3};

>> use entertainment; 
CREATE TABLE movies(
id int PRIMARY KEY,
title text,
year int,
rating text,
director text
);

>> COPY entertainment.movies(id,director,rating,title,year) FROM 'partial_data.csv' WITH DELIMITER=',' AND HEADER=TRUE;

>>> ![Import ‘partial_data.csv’ into cassandra server](./Images/12-cassandra-import.jpg)

## Task 13 - Write a cql query to count the number of rows in the ‘movies’ table
>> select count(*) from movies;

>>> ![a cql query to count the number of rows](./Images/13-cassandra-query.jpg)

## Task 14 - Create an index for the “rating” column in the ‘movies’ table using cql

>> create index rating_index on movies(rating);

>>> ![Create an index for the “rating”](./Images/14-cassandra-index.jpg)

## Task 15 - Write a cql query to count the number of movies that are rated ‘G’
>> select count(*) from movies where rating = 'G';
 
>>> ![A cql query to count the number of movies that are rated ‘G’](./15-cassandra-query.jpg)