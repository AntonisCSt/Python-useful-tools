### Sources: 
* https://towardsdatascience.com/python-decorators-for-data-science-6913f717669a
* https://www.youtube.com/watch?v=tfCz563ebsU&list=PLzMcBGfZo4-kwmIcMDdXSuy_wSqtU-xDP&index=4


### Basic useful decorators:

* Retry

```Python
@retry(max_tries=5, delay_seconds=2)
def call_dummy_api():
    response = requests.get("https://jsonplaceholder.typicode.com/todos/1")
    return response
```

* Caching

```Python
@memoize
def fibonacci(n):
    if n <= 1:
        return n
    else:
        return fibonacci(n-1) + fibonacci(n-2)
```

```
Function slow_fibonacci took 53.05560088157654 seconds to run.
Function fast_fibonacci took 7.772445678710938e-05 seconds to run.
```
* Timing

```Python
@timing_decorator
def my_function():
    # some code here
    time.sleep(1)  # simulate some time-consuming operation
    return
```

output:
```
my_function()

>>> Function my_function took 1.0019128322601318 seconds to run.
```

* Logging

```Python
@log_execution
def extract_data(source):
    # extract data from source
    data = ...

    return data

@log_execution
def transform_data(data):
    # transform data
    transformed_data = ...

    return transformed_data

@log_execution
def load_data(data, target):
    # load data into target
    ...

def main():
    # extract data
    data = extract_data(source)

    # transform data
    transformed_data = transform_data(data)

    # load data
    load_data(transformed_data, target)
```

```
INFO:root:Executing extract_data
INFO:root:Finished executing extract_data
INFO:root:Executing transform_data
INFO:root:Finished executing transform_data
INFO:root:Executing load_data
INFO:root:Finished executing load_data
```
* Notifying

```Python
@email_on_failure(sender_email='your_email@gmail.com', password='your_password', recipient_email='recipient_email@gmail.com')
def my_function():
    # code that might fail
```

### Multiple decorators

```Python
@log_execution
@timing_decorator
def my_function(x, y):
    time.sleep(1)
    return x + y
```