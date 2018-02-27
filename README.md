
[![Build Status](https://travis-ci.com/SPSCommerce/xd-transformation-service.svg?token=MzkqWQyz5MMM3E8CzXMi&branch=master)](https://travis-ci.com/SPSCommerce/xd-transformation-service)

### /transformation/<map_name>/<range_key>

description: get a transformation

method: GET

response:  200
```
{
    input_filename: file_name,
    timeout_status: true | false,
    sender: sender, 
    callback: Default Empty,
    parcel_uid: Default Empty,
    receiver: receiver,
    range_key: Unique ID,
    parcel_sender: Default Empty,
    transformation_status: ERROR | SUCCESS,
    end_time: end time,
    timeout: Default 180 seconds,
    branch: branch name,
    map_name: Map Name,
    transformation_state: PROCESSING | COMPLETE,
    parcel_receiver: Default Empty,
    user_name: user email addr,
    output_files: {
        filename: presigned_url to s3 location
        ...
        more files
    }
}
```

### /transformation/<map_name>?query_params

description: query transformations

method: GET

query_params

* f = field to query
* v = value
* o = operation

possible operations

* eq = equals
* lt = less than
* gt = greater than
* ge = greater than or euqal too
* le = less than or euqal too

query multiple fields by appending a number to the keys above (must start with 1).

example
```
?f1=user_name&v1=srussell@spscommerce.com&o1=eq&f2=branch...
```

response: 200
```
{
    [
        {


### /transformation/<map_name>/<range_key>

description: update a transformation

method: POST

request body: Pass any attributes you want updated.

example
```
{
    transformation_status: SUCCESS,
    transformation_state: COMPLETE
}
```

:
```
{
    maps: {[
        List of 2 maps objects (you can send more but nothing happens with them)
        ... (See map object below)
    ]},
    input: {[
        List of input objects
        ... (See input object below)
    ]}
}
```
response: 200
```
{
    map_name: name,
    start_time: time,
    user_name: user,
    left_branch: branch,
    right_branch: branch,
    job_id: parcel finder job id,
    diff_status: success | processing | error,
    report_url
}
```

### /diff/<map_name>/<start_time>

description: get a diff

method: GET

response:  200
```
{
    map_name: name,
    start_time: time,
    user_name: user,
    left_branch: branch,
    right_branch: branch,
    job_id: parcel finder job id,
    diff_status: success | processing | error,
    report_url
}
```

### /diff/<map_name>?query_params

description: query transformations

method: GET

query_params

* f = field to query
* v = value
* o = operation

possible operations

* eq = equals
* lt = less than
* gt = greater than
* ge = greater than or euqal too
* le = less than or euqal too

query multiple fields by appending a number to the keys above (must start with 1).

example
```
?f1=user_name&v1=srussell@spscommerce.com&o1=eq&f2=branch...
```

response: 200
```
{
    [
        {
            map_name: name,
            start_time: time,
            user_name: user,
            left_branch: branch,
            right_branch: branch,
            job_id: parcel finder job id,
            diff_status: success | processing | error,
            report_url
        },
        {
            map_name: name,
            start_time: time,
            user_name: user,
            left_branch: branch,
            right_branch: branch,
            job_id: parcel finder job id,
            diff_status: success | processing | error,
            report_url
        },
        ...
    ]
}
```

### Map and Input objects

xd-transformation-service supports sending map and input data in multiple ways.

#### Map

A map can either local xtl data or the remote repo location in xd-server

##### local xtl data
```
{
    input: source,
    output: target,
    branch: develop,
    sender: testsender,
    receiver: testreceiver,
    preferences: {
        ... See [Preferences](#preferences) object below
    }
}
```
##### remote xd-server location
```
{
    path: H065Costco.TnC.test.ag.to4010.agFedsWrite/loop/agFedsWrite.xtl,
    sender: testsender,
    receiver: testreceiver,
    branch: loop
}
```
#### Input

Map input can be send in three ways

###### Locally input data

```
{
    input_file: inputdata,
    file_name: test.txt
}
```

###### Remote xd-server location

```
{
    path: H065Costco.TnC.test.ag.to4010.agFedsWrite/new_dev/agFedsWrite.xtl,
    input_filename: input1.txt
}
```

###### Parcel ID

```
{
    parcel_uid: parcel_uid,
    parcel_service_env: dev | test | stage | preprod | prod
}
```

#### Preferences
It is an optional parameter that can be sent with the following attributes:
```
{
    enabled: "true" | "false",
    environment: test | preprod | prod
}
```
