# aws_tagging_policies
Implement AWS tag policies on an AWS Organization

## First example

### Create OUs
Log into management account, navigate to AWS Organizations and create an OU for the accounts that will be under the tagging policy (In this tutorial we will set up a policy on an OU, it can be set on the Organization level as well).

### Enable services in Organization
Navigate to Policies tab, enable Tag Policies

### Create and attach a tag policy
The tag policy example is for tagging EC2 instances (tag_policy.json), Create the policy with the file content.
Attach the tag policy to the OU created in the previous section.

### Move an account to the OU
Move an AWS account into the created OU

### Test the policy
Log in to the account, go to EC2 and create an instance with a tag - the tag is CostCenter, try a wrong value (for example 150) and you will see an error.


<img width="1995" alt="image" src="https://github.com/Issac87/aws_tagging_policies/assets/39260537/c075790f-e809-4ee3-97f3-b90d3bff4ab5">

When inputing one of the correct values (100/200) the resource the instance will be created successfully!

# Note - after this, it is still possible to create an instance without the tag, the enforcement is on the tag value but not the tag existence - for this we have the next section.

## Tag policy + SCP (Service Control Policy) implementation - enforce tag on resources.

### Create an SCP
Go to Policies and click on Service Control Policies, enable it, fill the content from the tag_scp.json file in the json input when creating the SCP.

### Attach SCP to the OU
Attach the SCP into the OU you previously created

### Test the policy
Log in the account under the OU and try to create an instance without a tag, you will see an error 

<img width="1934" alt="image" src="https://github.com/Issac87/aws_tagging_policies/assets/39260537/a96cb74e-a5e2-4fe0-9f83-b6c966195f7e">

If you try to create an instance with the CostCenter tag but with a wrong value (Value not in the list you provided in the Tag Policy) you will get another error: 

<img width="1979" alt="image" src="https://github.com/Issac87/aws_tagging_policies/assets/39260537/ea2d9016-db5f-43f3-b034-322e0cb53df8">


When creating the instance with the correct tag and one of the values from the list, the instance will be created successfully! 

In this tutorial the policy applies only to EC2 instances, however it can be set cross account (To all supported services which are most services in AWS).





