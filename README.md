# STEPS  
0. Clone this repo (lol I didn't have to tell you this 😂)
1. Deploy a bucket with `aws cloudformation deploy --stack-name old-bucket --template-file ./infra/old_bucket.yml --tags project=udapeople`    
    a. Set the S3 bucket name in the old_bucket.yml as any globally unique name you want, say xxx-bucket-123  
2. Upload the index.html into the bucket  
3. Deploy cloudfront (replace the S3BucketName value with the name of your bucket) with `aws cloudformation deploy --stack-name cloudfront --template-file ./infra/cloudfront.yml --tags project=udapeople --parameter-overrides S3BucketName=xxx-bucket-123`  
4. Push your changes to git to activate the workflow  

## What does the workflow do?
1. Creates a new bucket starting with new-bucket-XXX  
2. Copies the files in this repo to the new bucket  
3. Switches the cloudfront origin to the new bucket  
4. Destroys the old bucket (xxx-bucket-123)  