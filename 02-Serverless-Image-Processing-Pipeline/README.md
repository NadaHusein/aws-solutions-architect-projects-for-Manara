\###Architecture Explanation



**Upload**



* User requests upload URL.
* API Gateway invokes Lambda.
* Lambda generates a pre-signed URL.
* User uploads image directly to S3 Source Bucket.



**Event Processing**



* S3 Event Notification sends a message to SQS.
* SQS buffers requests and protects against traffic spikes.
* Lambda polls SQS.



**Workflow**



Step Functions orchestrate:



1-Validate image

2-Resize image

3-Add watermark

4-Store processed image

5-Save metadata to DynamoDB

6-Publish SNS notification



**Delivery**



Processed images are stored in Destination Bucket.

CloudFront caches images globally for fast access.



**Failure Handling**



Failed messages are retried automatically.

After retry limit, messages move to DLQ.



**3. AWS Services Used**



S3 Source Bucket => Store uploaded images

API Gateway =>	Upload endpoint

Lambda => Generate pre-signed URL \& image processing

SQS =>	Queue processing requests

DLQ =>	Store failed jobs

Step Functions => Coordinate processing workflow

DynamoDB =>	Store image metadata

SNS =>	Send notifications

S3 Destination Bucket => Store processed images

CloudFront =>	Deliver images globally



**4. Security**



* IAM Roles with least privilege.
* S3 Bucket Policies.
* Server-side encryption.
* Block Public Access on S3.
* CloudFront Origin Access Control (OAC).
* API Gateway authentication (optional).



**5. Scalability**



* Lambda scales automatically.
* SQS absorbs bursts.
* CloudFront reduces origin load.
* DynamoDB auto scaling.
* Serverless architecture requires no server management.



**6. Cost Optimization**



* Pay only per Lambda invocation.
* S3 Lifecycle transitions old images to cheaper storage classes.
* CloudFront caching reduces S3 requests.
* SQS charges per request.
* No EC2 instances to maintain

