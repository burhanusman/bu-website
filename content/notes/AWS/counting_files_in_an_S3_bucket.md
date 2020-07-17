# Counting Files in an S3 bucket


```python
import boto3
```


```python
bucket_name="bkt_name" #change the bucket name here
s3 = boto3.resource('s3')
bucket = s3.Bucket('project-pulse-transcribe-output')
```

### Get count of files in the bucket


```python
count=0
for item in bucket.objects.all():
    count+=1
print("Total Files in the bucket: ",count)
```

### To get all the file names in the bucket



```python
all_files=list(bucket.objects.all())
```

### To get all the keys in the bucket


```python
all_keys=[item.key.split(".")[0] for item in all_files]
```
