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
  -r    Repository name (Required)
  -e    Elasticsearch host (default: localhost:9200)
  -i    Elasticsearch indices name in the multiple index syntax https://www.elastic.co/guide/en/elasticsearch/reference/current/multi-index.html (default: all available)
  -s    Snapshot name (default: current time in %d-%m-%Y_%H:%M:%S:%3N format )
```
##EXAMPLES:
``` bash 
  python elasticsearch-snapshot.sh  -e "localhost:9200" -r "my_backup" -i "articles,users"
```
  This uses http://localhost:9200 to connect to elasticsearch and backs up the indices articles and users to an existing my_backup repository
  
``` bash 
  python elasticsearch-snapshot.sh  -e "127.0.0.1:9200" -r "my_backup" -i "logstash*"
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


