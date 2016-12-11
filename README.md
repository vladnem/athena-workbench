## CLI SQL for AWS Athena using SQL Workbench

The AWS account requires access to Athena and the staging dir where intermediary files are stored.

# Running script inline:

```
docker run --rm vladnem/athena-workbench \
	-url=jdbc:awsathena://athena.<AWS Athena Region>.amazonaws.com:443/AwsDataCatalog/<Database> \
	-connectionProperties='s3_staging_dir=s3://<Staging Bucket>' \
	-username=<AWS Access Key> \
	-password=<AWS Secret Key> \
	-command='select timestamp, elbname, requestip, requestport, backendip  from elb_logs limit 10;'
```

# Running scripts in external files:

```
docker run --rm vladnem/athena-workbench \
	-url=jdbc:awsathena://athena.<AWS Athena Region>.amazonaws.com:443/AwsDataCatalog/<Database> \
	-connectionProperties='s3_staging_dir=s3://<Staging Bucket>' \
	-username=<AWS Access Key> \
	-password=<AWS Secret Key> \
	-command="`cat scripts/test.sql`"
```
