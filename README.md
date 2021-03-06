```
export CFN_ARTIFACTS_BUCKET=<your-bucket-name>

# Create an S3 bucket for storing the processed templates, if you don't have
# one already (otherwise you can skip this)
aws s3 mb s3://$CFN_ARTIFACTS_BUCKET

# Package all the templates
aws cloudformation package \
    --template-file ./templates/main.yaml \
    --s3-bucket $CFN_ARTIFACTS_BUCKET \
    --output-template-file ./templates/processed.yaml

# And now deploy them (you can skip the --tags parameter if you want)
aws cloudformation deploy \
	--stack-name ec2-cloudformation-bg \
	--template-file ./templates/processed.yaml \
	--capabilities CAPABILITY_IAM
```
