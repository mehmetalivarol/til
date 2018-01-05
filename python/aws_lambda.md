AWS Lambdas have [in-memory filesystems](https://docs.aws.amazon.com/lambda/latest/dg/limits.html) (512 MB)  
that you can use for the duration of the lambda runtime. They're useful for file manipulation outside of S3. I had a case where I needed to zip a small piece of code from a file in S3, and store the resulting archive in S3, and the lambda was the perfect way to do that. 


```python
import boto3

import os
import tempfile
import zipfile

glue_client = boto3.client('glue', region_name='us-east-1')
s3_client = boto3.client('s3', region_name='us-east-1')
lambda_client = boto3.client('lambda', region_name='us-east-1')
s3 = boto3.resource('s3')

def lambda_handler(event, context):
    
    # pass in bucket/key from test event trigger

    record = event['Records'][0]
    bucket_name = record['s3']['bucket']['name'] # bucket 
    key = record['s3']['object']['key'] # filename
    
    tmp_dir = tempfile.gettempdir()

    # tmp_dir + filename
    path = os.path.join(tempfile.gettempdir(), key)
    
    # move .py file from S3 to local lambda storage
    s3.Bucket(bucket_name).download_file(key, path)
    print("file moved to /tmp")

    # show lambda dir contents to make sure it was moved correctly
    print(os.listdir(tmp_dir))
    
    # create a .zip file archive name
    archive = '%s/%s.zip' % (tmp_dir, key)
    
    # move file to archive
    with zipfile.ZipFile(archive, 'w')  as myzip:
        myzip.write(path,key) #don't want to nest folders
        print(zipfile.ZipFile.namelist(myzip))
    
    #upload zipped file to same S3 bucket
    s3_client.upload_file(archive, bucket_name, '%s.zip' % key)
```
