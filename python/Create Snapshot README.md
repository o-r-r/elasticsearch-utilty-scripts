#Elasticsearch Create Snapshot
[elasticsearch-snapshot.py](https://github.com/o-r-r/elasticsearch-utilty-scripts/blob/master/python/elasticsearch-snapshot.py)

Create a restorable snapshot of an elasticsearch index to an exiting repository

##USAGE: 
``` bash 
python elasticsearch-snapshot.py -r <repository name> [OPTIONS]
```

OPTIONS:
```
  -h    Show this message
  --repository    Repository name (required)
  --prefix        prefix to indices filter (required)
  --host          host, default : localhost
  --port          port, default : 9200
```
##EXAMPLES:
``` bash 
  python elasticsearch-snapshot.py  --host "localhost" --port "9200" --repository "my_backup" --prefix "articles,users"
```
  This uses http://localhost:9200 to connect to elasticsearch and backs up the indices articles and users to an existing my_backup repository
  
``` bash 
  python elasticsearch-snapshot.py  -host "127.0.0.1" --repository "my_backup" --prefix "logstash*"
```

  This uses http://127.0.0.1:9200 to connect to elasticsearch and backs up
  all of the logstash indices to an existing my_backup repository

##REQUIREMENTS:

* python
* pip : ``sudo yum install python-pip``
* elasticsearch-py: ``pip install elasticsearch``
* curator : ``pip install elasticsearch-curator``
* the aws cloud plugin https://github.com/elastic/elasticsearch-cloud-aws

You need to create an S3 repository for backing up the data to.
curl this to your elasticsearch cluster:

``` bash
PUT _snapshot/testing
{
  "type": "s3",
  "settings": {
    "bucket": "bucket_name" ,
    "base_path" : "backups/es",
    "endpoint" : "s3.amazonaws.com"
  }
}
```


