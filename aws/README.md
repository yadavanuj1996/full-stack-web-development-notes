
## IAM - Identity and access management

- An IAM identity provides access to an AWS account
- A user group is a collection of IAM users managed as a unit
- An IAM identity represents a user, and can be authenticated and then authorized to perform actions in AWS.
- Each IAM identity can be associated with one or more policies
- Policies determine what actions a user, role, or member of a user group can perform, on which AWS resources, and under what conditions.



### IAM Users
An IAM user is an entity that you create in AWS. The IAM user represents the person or service who uses the IAM user to interact with AWS.
A primary use for IAM users is to give people the ability to sign in to the AWS Management Console for interactive tasks and to make programmatic 
requests to AWS services using the API or CLI.


IAM User -> IAM User group (Policies are attached on the User Group)

Policies can be attached on the IAM User but it is not a best practice, the best practice is to assign a user in a user group and
then providing policies to IAM User group.

### IAM User Groups
An IAM user group is a collection of IAM users. You can use user groups to specify permissions for a collection of users, which 
can make those permissions easier to manage for those users. For example, you could have a user group called Admins and give that 
user group the types of permissions that administrators typically need. Any user in that user group automatically has the permissions
that are assigned to the user group.


### IAM roles
An IAM role is very similar to a user, in that it is an identity with permission policies that determine what the identity can
and cannot do in AWS. However, a role does not have any credentials (password or access keys) associated with it. Instead of
being uniquely associated with one person, a role is intended to be assumable by anyone who needs it. An IAM user can assume a role 
to temporarily take on different permissions for a specific task. A role can be assigned to a federated user who signs in by using 
an external identity provider instead of IAM. AWS uses details passed by the identity provider to determine which role is mapped to
the federated user.



### When to create an IAM user (instead of a role)
Because an IAM user is just an identity with specific permissions in your account, you might not need to create an IAM user for every
occasion on which you need credentials. In many cases, you can take advantage of IAM roles and their temporary security credentials instead 
of using the long-term credentials associated with an IAM user.

- You created an AWS account and you're the only person who works in your account.
- Create IAM users for the individuals who need access to your AWS resources, assign appropriate permissions to each user, and give each user his or her own credentials. We strongly recommend that you never share credentials among multiple users.


### When to create an IAM role (instead of a user)
- You're creating an application that runs on an Amazon Elastic Compute Cloud (Amazon EC2) instance and that application makes requests to AWS
- You're creating an app that runs on a mobile phone and that makes requests to AWS.
- Users in your company are authenticated in your corporate network and want to be able to use AWS without having to sign in again—that is, you want to allow users to federate into AWS.

### How AWS identifies an IAM user
- A "friendly name show in management console" for the user such as Richard or Anaya.

- An Amazon Resource Name (ARN) for the user. You use the ARN when you need to uniquely identify the user across all of AWS. ex:-
arn:aws:iam::account-ID-without-hyphens:user/Richard

- A unique identifier for the user. This ID is returned only when you use the **API**, Tools for Windows PowerShell, or **AWS CLI** to create the user; you do not see this ID in the console.

### Users and credentials
- Console password: A password that the user can type to sign in to interactive sessions such as the AWS Management Console. Disabling the password (console access) for a user prevents them from signing in to the AWS Management Console using their user name and password. It does not change their permissions or prevent them from accessing the console using an assumed role.
- Access keys: A combination of an access key ID and a secret access key. You can assign two to a user at a time. These can be used to make programmatic calls to AWS. If the user has active access keys, they continue to function and allow access through the AWS CLI, Tools for Windows PowerShell, AWS API, or the AWS Console Mobile Application.
- SSH keys for use with CodeCommit
- Server certificates

You can choose the credentials that are right for your IAM user. When you use the AWS Management Console to create a user, you must choose to at least include a console password or access keys. By default, a brand new IAM user created using the AWS CLI or AWS API has no credentials of any kind. You must create the type of credentials for an IAM user based on the needs of your user.

### Permissions Boundary
You can also add a permissions boundary to your users. A permissions boundary is an advanced feature that allows you to use AWS managed policies to limit the maximum permissions that an identity-based policy can grant to a user or role.


### Example scenario using separate development and production accounts
![roles-usingroletodelegate](https://user-images.githubusercontent.com/22169012/175478547-13706e92-001e-4766-815e-b24f8887e0bd.png)


### AWS IAM Access Analyzer
AWS IAM Access Analyzer provides the following capabilities:
- Access Analyzer helps identify resources in your organization and accounts that are shared with an external entity.
- Access Analyzer validates IAM policies against policy grammar and best practices.
- Access Analyzer generates IAM policies based on access activity in your AWS CloudTrail logs.

#### AWS Service Role
Many AWS services require that you use roles to control what that service can access. A role that a service assumes to perform actions on your behalf is called a service role. When a role serves a specialized purpose for a service, it can be categorized as a service role for EC2 instances, or a service-linked role. 

```
A role requires two policies: a role trust policy that specifies the principal that is allowed to assume 
the role and a permissions policy that specifies what can be done with the role. A role trust policy
is the only type of resource-based policy in IAM. Other AWS services have resource-based policies, such
as an Amazon S3 bucket policy.
```
