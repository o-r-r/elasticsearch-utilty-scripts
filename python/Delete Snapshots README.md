#Delete Snapshots
Delete snapshots from elasticsearch by date, with an option to skip deletion if no new snapthos would be found.

##USAGE

```bash
elasticsearch-delete-snapshot.py  -r <repository> -o <older_than> -i <ignore_if_newer_not_exist> -t <timestring>
```
OPTIONS:
```
  --repository  repository name (required)
  --timestring  timestring of the datestamp in an index name (required)
  --older_than  older than [ days ] (required)
  --ignore_if_newer_not_exist  don't perform deletion if there are no snapshots newer than this range [ days ] (required)
  --host  host, default : localhost
  --port  port, default : 9200
  -h  show this message
```
This will delete any snapshot that is older than than older_than days. 
However, The script will not delete any snapshot if there are no snapshot availabe that are newer than ignore_if_newer_not_exist parameter to maintain a certain level of data retention.

##EXAMPLES:
```bash
python elasticsearch-delete-snapshot.sh  -r my_backup -o 30 -i 10 -t %Y%m%d
```

Delete all snapshots in my_backup repository that are older than 30 days as long as we have snapshots from the last 10 days. Time filtering is done by the time string that should exist in the snapshot name.

##REQUIREMENTS:

* python
* pip : sudo yum install python-pip
* elasticsearch-py: pip install elasticsearch
* curator : pip install elasticsearch-curator
* the aws cloud plugin https://github.com/elastic/elasticsearch-cloud-aws

create an S3 repository:
```bash
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
