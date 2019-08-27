# PySpark에수 dataframe map() 사용

``` python
words = sc.parallelize (
   ["scala", 
   "java", 
   "hadoop", 
   "spark", 
   "akka",
   "spark vs hadoop", 
   "pyspark",
   "pyspark and spark"]
)
words_map = words.map(lambda x: (x, 1))

dataFrame.map(lambda x: (x, 1)) # error
dataFrame.rdd.map(lambda x: (x, 1)) # success
```

### 실수

> sparkContext.parallelize()의 리턴이 dataFrame이라고 착각

### 해결 방법
> sparkContext.parallelize()의 리턴은 rdd이다.

## reference

https://stackoverflow.com/questions/49243719/
