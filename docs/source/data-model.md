# Data model

There are multiple strategies to design your feature store schema. 
In this tutorial, we cover two of these strategies: wide table design and narrow table design.

## Wide table design

Here's an example table definiton that uses wide table design:

```sql
create table feature_store.flight_features(
	FL_DATE TIMESTAMP,
	OP_CARRIER TEXT,
	OP_CARRIER_FL_NUM INT,
	ORIGIN TEXT,
	DEST TEXT,
	CRS_DEP_TIME INT,
	DEP_TIME FLOAT,
	DEP_DELAY FLOAT,
	TAXI_OUT FLOAT,
	WHEELS_OFF FLOAT,
	WHEELS_ON FLOAT,
	TAXI_IN FLOAT,
	CRS_ARR_TIME INT,
	ARR_TIME FLOAT,
	ARR_DELAY FLOAT,
	CANCELLED FLOAT,
	CANCELLATION_CODE TEXT,
	DIVERTED FLOAT,
	CRS_ELAPSED_TIME FLOAT,
	ACTUAL_ELAPSED_TIME FLOAT,
	AIR_TIME FLOAT,
	DISTANCE FLOAT,
	CARRIER_DELAY FLOAT,
	WEATHER_DELAY FLOAT,
	NAS_DELAY FLOAT,
	SECURITY_DELAY FLOAT,
	LATE_AIRCRAFT_DELAY FLOAT,
	PRIMARY KEY (OP_CARRIER_FL_NUM)
);
```

As you can see this table has a lot of columns because each feature is
represented in a separate column. Consequently, whenever you want to add a new feature
in your feature store, you'll need to change the schema as well by adding a new column as well.
If you have many more features that you want to store and don't want to keep
changing the schema in cas you add a new one, you might want to try a narrow table design instead.


## Narrow table design

Here's an example table definiton that uses narrow table design:
```sql
create table feature_store.flight_features_narrow (
	OP_CARRIER_FL_NUM INT,
	FL_DATE TIMESTAMP,
	FEATURE_NAME TEXT,
	FEATURE_VALUE FLOAT,
	PRIMARY KEY (OP_CARRIER_FL_NUM)
)
```

In this example, you see just a few columns in the table. Aside from the
`OP_CARRIER_FL_NUM` and `FL_DATE` columns, which are specific to this example use case, 
the two other columns are general feature columns that can be used to store
any number of different features in just two columns. This type of design is
more flexible and requires no schema changes in case of adding or removing features
from the database.