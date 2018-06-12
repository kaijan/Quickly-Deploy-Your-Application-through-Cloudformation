# Quickly Deploy Your Application through CloudFormation



## Scenario
The following procedures help you quickly deploy your application through AWS CloudFormation. Modify a YAML script so that it will change original security group inbound rule, and then to confirm the update stack become effective.


## Prerequisites
>The workshop’s region will be in ‘N.Virginia’

>Sign-in a AWS account, and make sure you have select N.Virginia region.

>Make sure you have an Amazon EC2 key pair in the N.Virginia region. If you don’t have, see below link:
>https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-key-pairs.html#having-ec2-create-your-key-pair

## Lab tutorial
### Run the Original Template
1.1.  Download the **workshop.yml** in the repository.

1.2. Open this file in a text editor (preferably one that is JSON- or YAML or AWS CloudFormation- aware). In the particular, note the following features of this file:.

* This template creates an EC2 security group for the instance to give you SSH access.
* You will try to change security group inbound rule and confirm change status in the following steps.

1.3. On the **Services menu**, click **CloudFormation**.

1.4. Click **Create Stack**.

1.5. On the **Select Template** page, click the **Upload a template to Amazon S3** option. Click **Choose File** or **Browse** and select the template that you have been saving on your local hard drive..

1.6. Click **Next**.

1.7. On the **Specify Detail** page, use the following values:

* Stack name: **SecurityGroupCFTemplate**
* **KeyName**: select an existing EC2 keypair

1.8. Click **Next**.

1.9. On the **Options** page, create tags to associate with the resources created by the Template.Enter the following values:
* Key: **Name**
* Value:**EC2Instance**

1.10. Click **Next**.

1.11. On the **Review page**, review your input, and then click **Create**.

1.12. On the **AWS CloudFormation Dashboard**, select the entry for your stack, and when the **Status** value on the **Events** tab is CREATE_COMPLETE, continue to the next procedure.

![1.png](/images/1.png)

1.13. On the **Services** menu, click **EC2**.

1.14. Click the **Running Instances** link.

1.15. Verify that your **EC2 Instance‘s** Security Groups is now only allow SSH traffic.

![2.png](/images/2.png)

### Change Security Group Inbound Rule to Template

2.1. Open your CloudFormation template just download in a text editor.

2.2. Search in the template for the string **SecurityGroupIngress**. Find the entire value of the below command:

	IpProtocol: tcp
    FromPort: '22'
    ToPort: '22'
    CidrIp: !Ref 'SSHLocation'

2.3. Copy the following text to replace above command in your template:

	IpProtocol: tcp
    FromPort: '80'
    ToPort: '80'
    CidrIp: 0.0.0.0/0

2.4. Save the template as text file.


### Update Your Existing Stack

3.1. On the **Services** menu, click **CloudFormation**.

3.2. Select the template **(SecurityGroupCFTemplate)** that you created earlier.

3.3. For **Actions**, click **Update Stack**.

3.4. On the **Select Template** page, click the **Upload a template to Amazon S3** option, click **Choose File**, and then select your modified template from your hard drive.

3.5.Click **Next**.

>Note: At this point, AWS CloudFormation may detect an error in your template. AWS CloudFormation can detect two types of errors before executing your template:

* Syntax errors. Common culprits of syntax errors are un balanced brackets and missing commas after an object within a JSON array. Editing your file with a text editor that supports syntax checking (“linting”) of JavaScript or JSON files can help detect and eliminate these errors early.

* Reference errors. AWS CloudFormation is intelligent about the way you refer to other elements within an AWS Template file. For example, if you try to use the Ref intrinsic function that before you can proceed further with creating your stack.

If you receive an error at this stage, use your text editor or IDE to attempt to
fix it; or ask your instructor for solve it.

3.6. On the **Specify Details** page, for BastionInstance, type t2.small.

3.7. Click **Next**.

3.8. On the **Options** page, do not change any values.

3.9. Click **Next**.

3.10. Review the summary of your changes, and then click **Update**.

3.11. The status of your stack will change to **UPDATE_IN_PROGRESS** while the update takes place. Wait until it says **UPDATE_COMPLETE** before proceeding to the next step.

![3.png](/images/3.png)

3.12. On the **Services** menu, click **EC2**.

3.13. Click the **Running Instances** link.

3.14. Verify that your **EC2Instance‘s** Security Groups is being update to allow HTTP traffic.

![4.png](/images/4.png)

## Conclusion

Congratulations! You now have learned how to:
* Use AWS CloudFormation to quickly deploy your application.
* Change yaml format template.
* Update existing stack.



