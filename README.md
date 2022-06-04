# BLUE GREEN DEPLOYMENT WITH CIRCLE CI, CLOUDFORMATION AND CLOUDFRONT
### Technologies
Infrastructure Automation - CloudFormation  
Continuous Integration - CircleCI  
Blue Green Deployment - CloudFront  

## Steps
0. Clone this repo (lol I didn't have to tell you this 😂)
### Model current infra
1. Deploy a bucket with `aws cloudformation deploy --stack-name old-bucket --template-file ./infra/old_bucket.yml`. Set the S3 bucket name in the old_bucket.yml as any globally unique name you want, say `xxx-bucket-123`. The default in the file is `udapeople-kelechi`  
2. Upload your website files (index.html, etc) into the bucket. Confirm that the static website is reachable via `http://xxxx-bucket-123.s2-website-{YOUR REGION}.amazonaws.com`  
3. Deploy cloudfront (replace the S3BucketName value with the name of your bucket) with `aws cloudformation deploy --stack-name cloudfront --template-file ./infra/cloudfront.yml`. Please confirm from the CloudFormation UI that the created stack (cloudfront) has an output of S3BucketName with the value of your bucket (in this case, `xxx-bucket-123`). If it shows something else, please run `aws cloudformation deploy --stack-name cloudfront --template-file ./infra/cloudfront.yml --parameter-overrides xxx-bucket-123`, replacing the parameter-overrides argument to your your bucket name.  

4. Make changes to the files in src/

### Make changes to the app
5. Push your changes to git to activate the CI workflow.  
After a few minutes/hours (depending on your edge-location) your changes should be visible on the cloudfront site

## What does the workflow do?
1. Creates a new bucket with name `new-bucket-XXX` (XXX is a random number).  
2. Copies the files in `./src/` to the new bucket  
3. Switches the cloudfront origin from the old bucket (blue) the new bucket (green)  
4. Destroys the old bucket (xxx-bucket-123)  