## CLI SQL on Athena using SQL Workbench

The AWS account requires access to Athena and the staging dir where intermediary files are stored.

# Running script inline:

```
docker run --rm vladnem/athena-workbench \
	-url=jdbc:awsathena://athena.<athena region>.amazonaws.com:443 \
	-connectionProperties='s3_staging_dir=s3://<staging bucket>' \
	-username=<AWS Access Key> \
	-password=<AWS Secret Key> \
	-command='select timestamp, elbname, requestip, requestport, backendip  from AwsDataCatalog.sampledb.elb_logs limit 10;'
```

# Running scripts in external files:

```
 docker run --rm vladnem/athena-workbench \
	-url=jdbc:awsathena://athena.<athena region>.amazonaws.com:443 \
	-connectionProperties='s3_staging_dir=s3://<staging bucket>' \
	-username=<AWS Access Key> \
	-password=<AWS Secret Key> \
	-command="`cat scripts/test.sql`"
```
