# Enabling CloudTrail Logging for Your AWS Account
## Preparation
### Set a unique suffix to use for the S3 BucketName
```
RANDOM_STRING=$(aws secretsmanager get-random-password \
--exclude-punctuation --exclude-uppercase \
--password-length 6 --require-each-included-type \
--output text \
--query RandomPassword)
```

### Create an S3 Bucket 
```
aws s3api create-bucket --bucket awscookbook903-$RANDOM_STRING
```

## Clean up 
### Delete the trail: 
```
aws cloudtrail delete-trail --name AWSCookbook903Trail
```

### Delete the all versions of the files in your S3 buckets using some helper python scripts provided in the code repository:
```
export EXPORTED_RANDOM_STRING=$RANDOM_STRING
test -d .venv || python3 -m venv .venv
source .venv/bin/activate
pip install boto3
python bucket-del.py
deactivate
rm -rf .venv
unset EXPORTED_RANDOM_STRING
```

### Unset the environment variable that you created manually: 
```
unset RANDOM_STRING
```