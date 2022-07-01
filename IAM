Grant access to AWS resources
## 4 Steps to secure your AWS Root account
- Enable multi-factor authentication on the root account
- Create an admin group for your administrator, and assign the appropiate permissions  to this group
- Create user accounts for your administrator 
- Add your users to the admin group

User -> a physical person
Group -> Job function, functions, such as administrator 
Roles -> Internal usage within AWS

### The principal of Least Privilege
Only assign a user the minimun amount of privileges they need to do their job

Assing permissions using iam policy documents consiting of JSON 
Policy documents ands how it works.
Permissions: 
```json
{
	"Version": "2012-10-17"
	"Statement": [
		{
			"Effect": "Allow",
			"Action": "*",
			"Resource": "**"
		}
	]
}
```
Policy documents:
- Groups
- Users
- Roles

- **IAM is universal**: It does not apply to regions at this time
- **The Root Account**: The account created when you first set up your AWS account and which has coiomplete admin acces. Secure it as soon as possible and do not use it to log day to day.
- **New users**: No permissions when first created


**Access key ID and secret access key are not the same as usernames and passwords**
You only get to view these once. If you lose them, you have to regenerate them .So, save them in a secure location
Always set up passwords rotations, you can create and customize your own password rotation policies

**IAM Federation**: You can combine your existing user account with AWS. For example, when you log on to your PC (usually using Microsoft Active Directory), you can use the same credentials to log in to AWS if you set up federation
**Identity Federation:** Uses the SAML standard, which is Active Directory
