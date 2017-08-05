# Query tool for Meetup.com

This uses the Meetup python bindings to query Meetup.com on multiple search terms and using multiple filters on the results

## Requirements:

Currently has the following dependencies, all available via pip

```
meetup.api
prettytable
pyyaml
```

You will also need an API key for Meetup.com, which you can find from the API link at the bottom of your Profile page

### Configuration

The script takes a single argument --config which requires a path to your yaml config file as described below. An example YAML file is included

```
query_meetup.py --config matt_test.yml
```

### Config file syntax

```
meetup:
    api_key: yourmeetupapikey
    name_filter: True
    member_filter: True
    event_filter: True
    freq_filter: False
    period_filter:False
    period: 12
    min_period: 4
    min_members: 300
    min_events: 4
    min_freq: 60
    search_keys:
        - openstack
        - mesos
        - docker
        - data science
        - kubernetes
        - flink
        - spark
        - microservices
        - cloud native
        - big data
        - cassandra
        - kafka
        - scala
        - hadoop
        - coreos
        - software circus
        - data engineering
        - devops
locations:
    UK:
        - Manchester
        - Bristol
        - London
        - Birmingham
    DE:
        - Hamburg
        - Berlin
output:
    types:
         - table
         - xlsx
    sheet_name: test.xlsx
```                

api_key - a valid API key for Meetup.com

name_filter - apply the defined search keys as a second pass against the actual name of a set of groups. Meetup.com's search API does full text search of body descriptions as well, so returns a lot of results. This gives a further element of specifity. Boolean.

member_filter - use the number of members filter. Boolean.

min_members - the minimum number of members the member filter will look for.

event_filter - use the number of events filter. Boolean.

min_events - the minimum number of events a returned group should have. This looks for past events over the entire life of the group.

freq_filter - use the frequency of events filter. Boolean

min_freq - the minimum frequency of events, counted as average days between events.

period_filter - use the period filter. Boolean.

period - period of time for the period filter in months. This is back from current date.

min_period - the minimum number of events that should have occurred within the defined period.

search_keys - list of search keys to use to search for groups. These are currently concatenated with OR for the purposes of the query.

locations - the locations to query. 

output

types  - output format. Spreadsheet and console table are supported

sheet_name - name of spreadsheet to create, this can be a full path

Spreadsheet output will create xlsx format, with a worksheet per country defined in your locations. Spreadsheet name can be defined in the config file as above. 
TODO freeze to binary, improve docs, improve ( add ) error checking 
