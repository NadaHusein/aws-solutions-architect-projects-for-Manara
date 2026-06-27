

**##Multi-Region Disaster Recovery with Route 53 Failover**



**Project Overview**



Describe a disaster recovery architecture where:



* Primary Region = us-east-1
* Secondary Region = eu-west-1
* Route53 automatically switches traffic
* Aurora Global Database replicates data
* S3 Cross Region Replication protects files
* DynamoDB Global Tables replicate application data
* Warm Standby EC2 environment scales up during failover



**Disaster Recovery Strategy Comparison**



**Strategy	 		RTO	 RPO	      Cost**



Backup \& Restore	    Hours	 Hours	       Low

Pilot Light	  	    Minutes	Minutes	     Low-Medium

Warm Standby		    Minutes	Seconds	       Medium

Multi-Site Active-Active    Near Zero	Near Zero	High



**Aurora Global Database**



Explain:



* Primary Writer
* Read Replica
* Cross Region replication
* Near-zero RPO



**S3 Cross Region Replication**



Explain:



* Versioning enabled
* Replication Rule
* IAM Role
* Automatic object replication



**DynamoDB Global Tables**



Explain:



* Active-active
* Multi-region writes
* Low latency



**Route53 Failover**



Explain:



* Health Checks
* Primary Record
* Secondary Record
* Failover Policy
* Low TTL



**Warm Standby**



Explain:



**Primary**:



**ASG**



Desired = 2



Min =2



Max =6



**Secondary:**



Desired =1



Min =1



Max =6



**After failover**



Desired =4



**Backup Strategy**



Include:



* AWS Backup Plan
* Daily snapshots
* Retention
* Cross-region backup vault



**Monitoring**



CloudWatch alarms



↓



EventBridge Rule



↓



Lambda



↓



Increase ASG Capacity



↓



Notify SNS (optional)





