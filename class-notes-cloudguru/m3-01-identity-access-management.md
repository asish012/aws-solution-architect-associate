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

## LAB 1: Identity Access Management ##

