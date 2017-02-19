Welcome to the AWS-Arch wiki!

# Sample AWS Architecture
We often meet start-ups that have built their application around a core business idea and have gained enough customer patronage that they want to focus on adding mobility aspect to their application. They are confident about being the next killer app and want to plan for rapid growth that will closely and adequately cater to their clientele. At the same time they are concerned about buying too much infrastructure upfront. 

# Background
A laundry list of the start-up's requirements would be
* Enter the mobility space, build apps for iOS, Android devices around our core API
* Manage user mobile identities 
* Syncronize user data across multiple devices
* Send PUSH notifications to mobile customers
* Scale to meet demand that is uncertain in nature
* Distribute load effectively against server infrastructure
* Self-healing infrastructure that recovers from failed instances
* Replicate and manage multiple environments for dev team to work on

## Architecture Diagram
We will try and explore AWS services available to come up with an architecture that will satisfy our start-up's needs.

![Architecture Diagram](https://github.com/spkash-co-in/AWS-Arch/blob/master/spkash-co-in%20AWS%20Arch.jpg)


***

## AWS Mobile Hub
AWS Mobile Hub service provides a significant value to organizations willing to enter the mobility space. Lets explore the multiple services that we can leverage to satisfy out start-up and have them on their way to their fantabulous app.

![Mobile Hub](https://github.com/spkash-co-in/AWS-Arch/blob/master/awsMobileHub.JPG)

### Auto-generate Mobile iOS/Android code
1. AWS Mobile Hub can be used to auto generate client side SDK
2. AWS Mobile Hub auto-creates cloud side Cognito Identity Pools & IAM roles/policies
3. Available options/features on SDK generation
 * User Sign-in
 * User Data Storage
 * App Analytics
 * Push Notifications

![SDKs](https://github.com/spkash-co-in/AWS-Arch/blob/master/supportedSDKs.JPG)






## AWS Cognito User Pools
### User Identity Management
1. Cognito Fully Managed User Directory can be used to create users (Standard+custom Attributes available)
2. Cognito User Pools can be used as Identity Authentication provider
3. Optionally Facebook/Twitter/Google/SAML can be used
(Table 3 - User Sign-in Identity Provider)

![3rdParty](https://github.com/spkash-co-in/AWS-Arch/blob/master/3rdParty.JPG)

## Registering users
1. Send Registration request
2. SMS/Email verification
3. Confirm registration
4. Successful registration
(Table 1 - Register, Sign-in)

## Sign-in
1. Authenticate (SRP)
2. Optional - CAPTCHA, custom 2FA
3. JWT Tokens ( Id+Access+Refresh)

## AWS Cognito Federated Identities
### Request AWS Credentials
1. Exchange JWT Tokens  for temp AWS Credentials from AWS Cognito Federated Identities (uses AWS Security Token Service)
2. Temp AWS Credentials (Access Key+Secret Key + Session Token) are provided

## Cognito Sync 
### User Cloud sync across devices
By selecting On for Generate Cognito Sync option in User Data Storage section in AWS Mobile Hub the generated SDK provides simple Key/Value based cloud sync option to client. 
With just a few lines of code this function can be achieved.
1. CongitoSyncManager
2. Dataset.put
3. Dataset.syncrhonize

## API Gateway
### Making the API request from mobile 
1. Sigv4 signed requests with AWS Credentials 
2. API Gateway verifies authorization for requested resources 
3. Allow on successful authorization
4. Exchange IAM credentials for user JWT

## Elastic Bean Stalk
### Autoscaling and Loadbalancing requests to server app
Assuming the startup is using a LAMP stack, it can be wrapped inside the Elastic Bean Stalk and capability-added to scale for demand. Moreover multiple environments dev/test/stage/prod can be spinned up easily creating a wholesome environment for the dev team to start cranking. And with the multiple deployment options available the devOps team is in for a treat as well.
1. Elastic Bean stalk can be used to create an App name with PHP platform 
2. Provide zip file or use  eb cli 
3. Elastic Bean stalk provides easy option for creating multiple environments (Dev, Test, Stage, Prod etc) 
4. Clone environments with simple mouse click 
5. Deployment policies can be selected as well 
6. Multi-AZ  Auto-scaling can be selected by mentioning Azs by name Cross-Zone ELB can be used for even load distribution 
7. Some configuration options listed below 
  * Autoscaling
    * Min/Max instances 
    * Placement Azs 
    * Scaling Trigger -CPU/Reqs metrics 
    * Auto scaling Health Check 
  * Application Deployment policy
    * Rolling w/additional batch
    * Batch size 
  * High-Availability 
    * ELB
    * HTTP/HTTPS SSL 
    * Cross Zone 
    * Connection 
    * ELB Health Check
  * Environment Properties 
    * External RDS settings

## Amazon RDS
### Highly Available Database Service
1. Master-Standby synchronous replication 
2. Read replicas as needed -asynchronous replication 
3. Automated backups Snapshots option
4. Choose Multi-AZ and make it highly available

## Route 53
### Disaster Recovery Policy
Depending on the start-up need and budget differt DR policies may be explored. Depending on client needs and RTO+ RPO requirements options range from
* Multi-site deploy in multiple regions active load servicing 
  * Multi-site deploy, Route 53 DNS failover over
* Warm standby
  * Options available like API Gateway -> CloudWatch Metrics -> Alarms -> Lambda -> CloudFormation execute
* Pilot
  * Consider RDS backups, restore from snapshots, Read replica 

## S3 and Glacier
### Archiving
1. Store objects in S3
2. Auto-rollover to cheaper Glacier for long-term archiving
3. Note the retrievl time differnce between S3 and Glacier and choose 

## SNS 
### Push Notifications to mobile app
Sending  notifications to better match mobile user needs forms a significant piece that the organization has to handle. SNS make this much simpler to implement.
1. Notifications to consumer (Pub/Sub)
2. Direct + Topic Publish, simple one-line code 
3. Options like APNS+GCM+ADM gateways for Push available 
4. SMS / Email also

## AWS Mobile Analytics
## Analytics on your customer base
Learning about your customer base usage patterns provides significant insight into the business areas that are protifable and those which needs attention. AWS Mobile Analytics make its very easy to gather stats.
1. AWS Mobile Hub generates SDK which pushes events to AWS Mobile Analytics service for mobile related analytics data
2. Embedding code on select code points, options for Custom events to gather user usage. 
3. Dashboards in AWS Mobile Analytics for all major data points 
4. Option  to stream analytics data to AWS Kinesis for more finetuned analysis, Tableau, Machine 

![Mobile Analytics](https://github.com/spkash-co-in/AWS-Arch/blob/master/mobileAnalytics.JPG)

![Export Analytics](https://github.com/spkash-co-in/AWS-Arch/blob/master/exportAnalytics.JPG)

## CloudWatch, AWS Lambda, CloudFormation
### Support services
Monitoring continuously and reacting to events or alarms keeps the infrastructure in top-shape. The above mentioned services combined together help achieve this goal.
1. Publish logs to Cloudwatch User Cloudwatch metrics to create Alarms 
2. Trigger some Lambda on alarm 
3. Lambda can execute CloudFormation template and take corrective action






    
