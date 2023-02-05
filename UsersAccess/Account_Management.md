## Purposes of an AWS account: 
- *Container*: basic container for AWS resources. Every resource in AWS is uniquely identified by an Amazon Resource Name that includes that account ID of the account that contains or owns the resource. 
- *Security Boundary*: provides security boundary for AWS resources - i.e. resources are only accessible to users who have the right credentials. 

## Do you need multiple AWS accounts: 
Short answer is yes. Long answer is: based on the AWS Well-Architected Framework, it is recommended to isolated resources and users to create a secure and well government organisation. Managing multiple AWS accounts is done through the global service AWS Organisations. 

## AWS Account Identifiers:
- AWS account ID - 12 digit numbers that uniquely identifies an AWS account. Many resources use AWS account ID in their ARN. 
- Canonical user ID - alphanumeric identifier that is an obfuscated form of AWS account ID. Use this ID to identify an AWS account when granting cross-account access to bucket and objects using S3 (only used by S3)

## Root user
- The account owner and is created when the AWS account is created. IAM users and IAM Identity Centre users are created by the root user or an admin for the account. 
- Root has security credential to access the all resources permitted to the account. To limit permission of the root user, the only method is to use Service Control Policy of AWS Organizations. 
- Recommended to create an admin user and only use root user for tasks that require root user's credentials. 

## Best practices for root users:
- Use MFA for root user
- Don't share password
- Use a strong password
- Create an IAM admin user for daily taks.
- Use root users for tasks that require root security credentials.
- Don't create access key for root user. In case having the root key is a must, rotate the key regularly. 

## What is AWS Access Key: 
When using AWS programmatically, AWS access key is required to verify user's identity. AWS access key consists of 
- Access Key ID 
- Secrete Access Key 

## Best Practices for AWS Access Key 
- Best way to protect account is to not have access keys for AWS root user. Second best way is to use IAM user access keys in place of roots.
- In many scenarios when long-term access keys that never expire are not needed (IAM user access keys or root user access keys), it is preferred to use IAM roles and generate temporary access keys (which has an expiry token).
- Some use-cases where an IAM role is preferred over IAM users:
  - Applications running on EC2 instance - define an IAM role with access to required resources and attached to an EC2 instance, then run the application on that instance. 
  - Cross-account accaess - use IAM role to establish trust between accounts then grant users in one account limited permissions to access the trusted account (Delegate access across AWS account with IAM roles)
- IAM user access key management best practices: 
  - Don't embedded directly to your code, but set them up as USER environment variables (in contrast to SYSTEM environment variables)
  - Different access keys for different applications
  - Rotate access keys regularly 
  - MFA for most sensitive applications.
  - Remove unused access key.

## Organisation Account Management
Use AWS Organization services to manage multiple accounts from an organisation. Administrative tasks are performed by the organisation's management account. The functionality that allows the management account to organise organisation can be extended to other services by using trusted access between Organizations and those services. This allows the services to access information about the organisations and the accounts it contains. When you enable trusted access for Account Management, the Account Management service grants Organizations and its management account permissions to access the metadata for all of the organization's member accounts.

After trusted access is enabled, choose a designated member account as a delegated admin account for AWS Account Management. This allows the delegated admin to perform Account Management metadata management tasks similar to the management account. The delegated admin doesn't have all administrative access to the organisation that the management account has, only management tasks priviledge. 

When an AWS account is part of an organisation, the admin of the organisation can apply Service Control Policies (SCPs) to limit what the principles in member accounts can do. SCPs doesn't grant permission, it is a filter that limits what permissions can be used by the member account. A user or role (a principal) an perform actions that are in the intersections of what is allowed by the SCPs and the IAM permission policies. 