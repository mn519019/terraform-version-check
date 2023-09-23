import json
import boto3
import os

# This script is developed to quickly identify terraform version for each module.
# It's assumed that your project stores tf statefile in the S3 bucket 

target_var="terraform_version"
file_list=[]

def prGreen(skk): print("\033[92m {}\033[00m \n" .format(skk))

def detect_current_region():
    global region
    region=os.environ.get('AWS_REGION')
    return region

# Get account ID to reference file
def get_account_id():
    # Make the bucket name global
    global bucket_name
    client = boto3.client("sts")
    res = client.get_caller_identity()["Account"]
    
    # Call the region detection function
    region = detect_current_region()
    # Lab
    if res == "YOUR-ACCOUNT-ID" and region == "us-east-1":
        bucket_name="tfstate-example-project-"+region+"-"+res
        print("example-projec1", region, "\n")
    elif res == "YOUR-ACCOUNT-ID" and region == "us-east-1":
        bucket_name="tfstate-example-project-stage-"+region
        print("example-projec2", region, "\n")
    else:
        print("Config is not matched. Please check your aws profile information") 
    return bucket_name

def list_files_s3():
    s3 = boto3.resource('s3')
    my_bucket = s3.Bucket(bucket_name)
    # print('================ Avaialable Files ================')
    for my_bucket_object in my_bucket.objects.all():
        object_key = my_bucket_object.key
        file_list.append(object_key)
    # print('==================================================')
    return file_list

# Terraform Version Check function from the S3 Bucket Object
def version_check(bucket_name):
    session = boto3.Session()
    s3_client = session.client("s3")    
    for x in range(len(file_list)):
        response = s3_client.get_object(Bucket=bucket_name, Key=file_list[x])
        file_content = response['Body'].read().decode('utf-8')
        json_content = json.loads(file_content)
        if target_var in json_content:
            print('File Name:',file_list[x])
            print("Terraform Version:", end="")
            prGreen(json_content[target_var])

# Running a script 
print('================ Account Info ================\n')   
get_account_id()
print('==============================================\n')
list_files_s3()
version_check(bucket_name)
