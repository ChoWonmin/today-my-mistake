# PySpark User-defined-funtion에서 return 값 사용하기

PySaprk에서 rest api를 호출하는 상황이었다.
udf 함수를 만들어서 rest api를 호출하여 결과를 받았다. return type이 기본적으로 string이었다.

``` python
# udf의 리턴 타입을 직접 작성해주어야한다.
my_func_return_type =  ArrayType(
                   StructType([StructField("sentence_id", LongType()),
                               StructField("sentiment", StringType()),
                               StructField("sentence", StringType()),
                               StructField("keywords", ArrayType(StringType())),
                              StructField("keywords_norm", ArrayType(StringType())),
                              StructField("tags", ArrayType(StringType()))])
)

my_func = udf(lambda contents: my_func(contents), my_func_return_type)
```
