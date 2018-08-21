### What is IAM? ###
IAM allows you to manage users and their level of access to the AWS Console.

### What does IAM proved? ###
- Centralized control of your AWS account.
- Shared access to your AWS account.
- Granular Permissions.
- Identity Federation (including Active Directory, Facebook, Linkedin etc)
- Multi-factor Authentication
- Provide temporary access for users/devices and services where necessary.
- Allows you to set up your own password rotation policy.
- Integrates with many different AWS services.
- Supports PCI DSS Compliance.

### Some Terms ###
- Users: End users (people)
- Groups: A collection of users under one set of permissions. HR group, Admin group, Finance group. Grouping users together and applying one or more sets of permissions together.
- Role: Roles are assigned to AWS resources. e.g. your EC2 instance might be assigned a role to get access to your S3 instance to write files directly (no need to set up username password for that EC2 instance)
- Policy: A document that defines one or more permissions. You can assign a policy to a User or a Group or a Role.

### LAB 1: Identity Access Management ###
IAM doesn't have a region, its Global. All your created Users, Groups, Roles, Policies and other components of IAM are available globally.

- Activate Multi-Factor-Authentication on your root account:
    - Your root account is the account associated with your email id in AWS.
    - Authenticate using Google-Authenticator on your Android device.
- Create some Users and Groups and assign those users into some Groups.
    - Once Users are created and assigned to some Groups, you will be able to see every user has been assigned a "Access key ID" and a "Secret access key". This key is used when the user wants to connect to AWS services programmatically (e.g. terminal of your laptop).
    - Every user will also be assigned a username and a password, which will be used when the user wants to login to the AWS Console.
- You can also add permissions to a particular user directly instead of via assigning him in a group and giving permission to the group.
- You can specifically Activate/Deactivate users programmatic access rights (Access key ID & Secret access key).
- You can also make change of your IAM password policy (e.g. password strength, expiration etc)

* IAM roles: IAM roles are a secure way to grant permissions to entities that you trust.

    Examples of entities:
    - IAM user in another account.
    - Application code running on an EC2 instance that needs to perform actions on AWS resources.
    - An AWS service that needs to act on resources in your account to provide its features.
    - Users from a corporate directory who use identity federation with SAML.

    We are planning to create an EC2 instance which will store data directly to S3 buckets.
    1. Create a role which will have full access to write to S3 bucket. While creating a Role we need to tell:
        - Whom is it for? (EC2),
        - What is it for? (Allows EC2 instances to call AWS services on your behalf),
        - and What AWS service will it access? (S3 full access)
    2. Create an EC2 instance and assign him the role we just created.
