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

### Auto-generate Mobile iOS/Android code
1. AWS Mobile Hub can be used to auto generate client side SDK
2. AWS Mobile Hub auto-creates cloud side Cognito Identity Pools & IAM roles/policies
3. Available options/features on SDK generation
 * User Sign-in
 * User Data Storage
 * App Analytics
 * Push Notifications
![AWS Mobile Hub ]( https://github.com/spkash-co-in/AWS-Arch/blob/master/spkash-co-in%20AWS%20MobileHub.JPG)







## AWS Cognito User Pools
### User Identity Management
1. Cognito Fully Managed User Directory can be used to create users (Standard+custom Attributes available)
2. Cognito User Pools can be used as Identity Authentication provider
3. Optionally Facebook/Twitter/Google/SAML can be used
(Table 3 - User Sign-in Identity Provider)

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
