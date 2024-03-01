
This follows information on iceberg.apache.org

#Startup
```docker-compose up```

#Pyspark
```docker exec -it spark-iceberg pyspark```


#Notebook server
```docker exec -it spark-iceberg notebook```

This will make a notebook server available at http://localhost:8888


#Sample Code
Create and write to a table in python
```
from pyspark.sql.types import DoubleType, FloatType, LongType, StructType,StructField, StringType
schema = StructType([
  StructField("vendor_id", LongType(), True),
  StructField("trip_id", LongType(), True),
  StructField("trip_distance", FloatType(), True),
  StructField("fare_amount", DoubleType(), True),
  StructField("store_and_fwd_flag", StringType(), True)
])

df = spark.createDataFrame([], schema)
df.writeTo("demo.nyc.taxis").create()

schema = spark.table("demo.nyc.taxis").schema
data = [
    (1, 1000371, 1.8, 15.32, "N"),
    (2, 1000372, 2.5, 22.15, "N"),
    (2, 1000373, 0.9, 9.01, "N"),
    (1, 1000374, 8.4, 42.13, "Y")
  ]
df = spark.createDataFrame(data, schema)
df.writeTo("demo.nyc.taxis").append()

df = spark.table("demo.nyc.taxis").show()
```

#Next Steps

1. Start docker desktop
2. In the git window run docker-compose up
3. In a new window, launch the pyspark session: 
```docker exec -it spark-iceberg pyspark```

From there, do the code shown above to watch the process work.
