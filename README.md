
[![Build Status](https://travis-ci.com/SPSCommerce/xd-transformation-service.svg?token=MzkqWQyz5MMM3E8CzXMi&branch=master)](https://travis-ci.com/SPSCommerce/xd-transformation-service)
### Map and Input objects

xd-transformation-service supports sending map and input data in multiple ways.

#### Map
[Preferences](#preferences)
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
