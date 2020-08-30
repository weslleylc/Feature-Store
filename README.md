# Feature-Store
A containerized approach using Apache Kafka, Spark, Cassandra, Hive,postgresql, Jupyter, and Docker-compose.

Medium link https://medium.com/@weslleylc/building-a-feature-store-4a2dffee17fe

Usage
-----

Clone the repo:

    git clone https://github.com/weslleylc/Feature-Store.git
    cd Feature-Store

Run docker-compose and wait until all containers have been instantiated.:

    docker-compose up -d
    
Open and run the following notebooks at spark/notebooks:
* Kafka.ipynb
* Starbucks_ETL.ipynb

The Kafka notebook will produce json kafka streming at topic queueing.transactions.
The Starbucks_ETL.ipynb will consume kafka topics and build the feature store.


Simulating the following scenario:
-----

We have a streaming JSON data source with events of Starbucks orders being captured in real-time.
We have a CSV data set with more information about drinks.

Objective:

We want to parse the JSON from the streaming source, performing aggregations operations, and store all rows in a cheap structure(like s3) and get more recent transactions on a low latency database like Cassandra.
We desire to have an output with the schema:

  * id_employer: int
  * name_employer: string
  * name_client: string
  * payment: string
  * timestamp: timestamp
  * product_name: string
  * product_size: string
  * product_price: int
  * percent_carbo: float
  * final_price: float

Solution using Butterfree library and the above architecture:
![alt text](https://github.com/weslleylc/Feature-Store/blob/master/spark/notebook/arc.png?raw=true)

  * Apache Kafka as data sources (Streaming input data);
  * A hive metastore to store metadata (like their schema and location) in a relational database. (For this tutorial we will use Postgresql)
  * Apache Cassandra to store more recent data.
  * Amazon S3 to store historical features or table views for debug mode.
