# SDLC Automation

## DevOps

DevOps integrates development and operations teams to improve collaboration and productivity by automating infrastructure, workflows, and continuously measuring application performance. It embodies a culture and set of practices that bring development and operations teams together to complete software development. It allows organizations to create and improve products at a faster pace than they can with traditional software development approaches.

## Benefits of Automation

- **Speed**: Accelerate the delivery of software and features.
- **Rapid Delivery**: Enable frequent and faster release of new features and bug fixes to improve product.
- **Reliability**: Ensure the quality and stability of application updates and infrastructure changes.
- **Scale**: Manage and operate your infrastructure and development processes at scale.
- **Improved Collaboration**: Enhance communication and collaboration among teams.
- **Security**: Integrate security measures into the software development lifecycle.

### Blue/Green Deployment

Blue/Green deployment is a technique that reduces downtime and risk by running two identical production environments. Only one of the environments is live at any given time, where the live environment serves all production traffic.

#### Key Points

- **Zero Downtime**: Deployments do not affect the application's availability.
- **CNAME Swapping**: Traffic is redirected to the new version by changing the CNAME record of the environment URL.
- **Route53 Integration**: Uses Amazon Route53 to manage the DNS switching.
- **Rapid Rollback**: Quick rollback to the previous version if necessary.
- **Database Decoupling**: The database should be separate to avoid data inconsistencies.

## AWS Lambda Blue/Green Deployments

#### Key Concepts

- **$Latest**: Represents the most recent version of your Lambda function.
- **Version**: An immutable snapshot of a Lambda function.
- **Lambda Alias**: Points to a specific Lambda version, enabling blue/green deployments by redirecting the alias.

### AWS Lambda Alias Traffic Shifting

AWS Lambda supports traffic shifting using aliases, allowing gradual transition of traffic from an old version to a new version. This feature facilitates testing in production and reduces the risk of introducing a new version.

### Blue/Green with Route53

Leverage Route53's weighted routing feature to gradually shift traffic between two environments (blue and green), providing a mechanism for safe, reversible deployments.

### Using AWS OpsWorks for Blue/Green Deployments

AWS OpsWorks supports blue/green deployments by creating and managing stacks, which are logical groups of AWS resources. By cloning an OpsWorks stack and deploying a new version, traffic can be redirected to the new stack using Route53.

## AWS CodeCommit

CodeCommit offers a fully managed source control service that hosts secure Git-based repositories.

### Key Features

- **Private Git Repositories**: Secure and scalable Git hosting.
- **Unlimited Repositories**: No size limits on repositories.
- **Highly Available**: Built to be highly available and durable.
- **Integration**: Works with popular CI tools like Jenkins and AWS CodeBuild.
- **Security**: Offers robust security features for your code.

### CodeCommit Security

- **Authentication**: Supports SSH keys and HTTPS for secure access.
- **Authorization**: Managed via IAM policies.
- **Encryption**: Ensures data is encrypted at rest and in transit.
- **Cross-Account Access**: Integration with EventBridge for cross-account repository replication.

#### IAM Policies for CodeCommit

- **AWSCodeCommitFullAccess**: Provides full access to CodeCommit repositories.
- **AWSCodeCommitPowerUser**: Allows users to modify code but not manage repositories.
- **AWSCodeCommitReadOnly**: Grants read-only access to repositories.

### CodeBuild

CodeBuild is a fully managed build service that compiles source code, runs tests, and produces software packages.

#### Key Concepts

- **buildspec.yaml**: Defines build commands and settings.
- **Environment Variables**: Configures the build environment.
- **VPC Support**: Allows CodeBuild to access resources within a VPC.
- **Security**: CodeBuild uses service roles to interact with other AWS services securely.

### CodeDeploy

Automates software deployments to various compute services such as Amazon EC2, AWS Fargate, AWS Lambda, and your on-premises servers.

#### Deployment Configurations

- **In-Place Deployment**: Updates applications on existing instances.
- **Blue/Green Deployment**: Launches a new version alongside the old version before switching traffic.

#### Lifecycle Hooks

- ApplicationStop - This deployment lifecycle event occurs even before the application revision is downloaded
- DownloadBundle - The codedeploy agent copies the application revision file to a temporary location.
- BeforeInstall* - you can use this hook for pre install tasks such as creating backup etc.
- Install - This hook will install the version from temp to final destination.
- AfterInstall - You can use this hook for configuraion or changing file permissions.
- ApplicationStart - This hook start the application if stopped.
- ValidateService - You can use this hook to verify the deployment completed.
- BeforeBlockTraffic - you can use this deployment lifecycle event to run tasks on instance before they were deregistered from loadbalancer.
- Blocktraffic*  - during this lifecycle hook the internet traffic is blocked from accessing instance that are currently serving traffic.
- AfterBlockTraffic - You can use tasks on instance after they are deregistered from loadbalancer
- BeforeAllowTraffic* - You can run tasks on instance after they registered with loadbalancer.
- AllowTraffic - Allow loadbalancer to server traffic and access instance.
- AfterAllowTraffic* - Run task son instance after they are registered with loadbalancer.

### CodePipeline

Automates the build, test, and deploy phases of your release process every time there is a code change, based on the release model you define.

#### Integration

- **CloudFormation**: Supports CloudFormation for infrastructure updates.
- **Multi-Region Deployments**: Facilitates deployments across multiple AWS regions.
- **Artifact Management**: Integrates with S3 for storing build

 artifacts.

## DynamoDB

### Basic Concept

- Base table
- Secondary Index

### Projection in Secondary Indexes

A projection refers to the set of attributes that are copied from the base table into secondary index. 

Base table have UserId and GameTitle , if we want to make more index i.e  Topscore , we can create secondary index. 

### Type of Projection

- KEYS_ONLY - > only kets of partition key , sort key are included.
- INCLUDE → this include key and other attributes
- ALL - Every attribute from the basic table is copied into the index.

### Deployment Types in Elastic Beanstalk

- All at once
- Rolling deployment
- Rolling deployment with additional batch
- Immutable deployment
- Traffic splitting deployment
- Blue/green

### Additional Tools

- **CodeGuru**: Offers intelligent recommendations to improve code quality.
- **AWS Amplify**: Streamlines the development of web and mobile applications.
