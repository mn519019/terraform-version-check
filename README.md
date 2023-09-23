# terraform-version-detection

## Background
In our organization, we use terraform & terragrunt to manage cloud resources. 
This script is compatible with AWS only for now. We keep our tf.state file in AWS S3 bucket. 
When it comes to maintain terraform resource, the version plays a key role, and thus we need to check the version. This script shows all the list of tf state files with the version using Python 3 boto module. Therefore, we don't need to visit every file to check the terraform version on the module.

## Requirements 
```
- AWS Login
- python3
- boto3 (Python Library)
- S3 Bucket Name 
- S3 Account ID (Integer)
```

## Customization for your project
This script checks your account number and region and find the matching bucket from AWS S3.
You would want to udpate the conditional statements as your project requires 
The customization can be done by updating the value in the if else block

An example is given below: 

``` 
if res == "260558396643" and region == "us-east-1":
        bucket_name="tfstate-mtd-staging-"+region+"-"+res
        print("MTD-STG", region, "\n")
elif res == "318798178487" and region == "us-east-1":
        bucket_name="tfstate-bb-dlp-stage-"+region
        print("DLP-STG", region, "\n")
```

## Implementation 
```
# Clone the project 
git clone https://gitlab.rim.net/rick_yang_script/terraform-version-detection.git](https://github.com/mn519019/terraform-version-check.git)
cd terraform-version-detection

# Check the Terraform version per each module
python3 tf-version-detection.py
================ Account Info ================

example-project1 us-east-1

==============================================

File Name: azs.tfstate
Terraform Version: 0.12.31

File Name: cluster-autoscaler.tfstate
Terraform Version: 0.12.26

File Name: ecr.tfstate
Terraform Version: 0.12.31

File Name: eks.tfstate
Terraform Version: 0.12.31

File Name: elasticsearch.tfstate
Terraform Version: 0.12.31

File Name: iam-assumable-role-with-oidc-cw-exporter.tfstate
Terraform Version: 0.12.26

File Name: iam-assumable-role-with-oidc.tfstate
Terraform Version: 0.12.26
```
