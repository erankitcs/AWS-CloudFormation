# Self Service App
This project is based on the concept of self service portal for Developers, Testers and PreSales guys who wants their infrastructure available on demand.
Hows that when the Presales team is presenting a demo and client requested for a different version of the application, Presales person just clicked a button and a verified and tested application with required infrastructure is spun up. Or even you want to develop a new feature of the application, you just hit a button and start coding on a standalone instance instead of having DEV/TEST version environments and multiple developers working on the same instance.
In this project, We solved three problems
- User has to enter shared infrastructure stack values like VPC Id and other => Solved using Inter Stack references.
- No test of application for success(creation policy) on updates of the stack. => Solved by using Autoscaling AutoScalingReplacingUpdate functionality.
- Manual inputs for the Subnets CIDR range for application stack. => Solved by using CustomResource in cfn which uses a Lambda with DynamoDB to generate valid CIDR range automatically during stack creation.

## Detailed Deployment
- First, deploy SharedInfrastructure using portalbucketanduser.yml
- then deploy Application codes and test code from APPS folder to App Bucket
- then deploy autosubnet.zip to lambda bucket
- Now, deploy AutoSubnet stack using autosubnet.yml
- Next, deploy PortalBucketandUser stack usin portalbucketanduser.yml
- upload appenv.yml into App bucket.
- finally, update portal.html with secret code and appenv.yml url and upload into App Bucket.
- Run Output URL of stack "PortalBucketandUser" to launch the portal.

### Architecture
![Screenshot](/SelfSerApp.jpeg)

### Website Demo
![Screenshot](/SelfServApp.gif)
