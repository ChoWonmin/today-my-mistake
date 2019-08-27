# SparkSession에서 SparkContext 접근

``` python
spark = SparkSession.builder.appName("test").getOrCreate() # SparkSession 생성
sc = spark.sparkContext # SparkSession에서 sparkContext로 접근
```

### 실수

> SparkSession.builder가 sparkContext를 리턴할 것으로 착각

### 해결 방법
> SparkSession.sparkContext로 접근해야한다.

## reference

https://datascience-school.com/blog/practical-apache-spark-in-10-minutes-part-2-rdd/

https://stackoverflow.com/questions/39535447/attributeerror-dataframe-object-has-no-attribute-map
