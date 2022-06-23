
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

