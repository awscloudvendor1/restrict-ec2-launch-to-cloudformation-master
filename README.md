# Restrict EC2 Launch Only through Cloudformation

Let us say you want users the privilege to launch stack which will deploy an ec2 instance for you, but only through cloudformation. How do you achieve it. We can provide this type of authorization using the `aws:CalledVia` condition key.

![Restrict EC2 Launch Only through Clouformation](images/restrict-ec2-launch-to-clouformation.png)

1. ## โ๏ธ Prerequisites

    This demo, instructions, scripts and cloudformation template is designed to be run in `us-east-1`. With few modifications you can try it out in other regions as well(_Not covered here_).

    - AWS CLI pre-configured - [Get help here](https://youtu.be/TPyyfmQte0U)

1. ## ๐ How does this work

    The following policy does the trick for us. The `condition` key in the statement checks, how the service is being called and only `ALLOW`s the request if it is made _via_ cloudformation.

    ```json
    "Condition": {
      "ForAnyValue:StringEquals": {
        "aws:CalledVia": [
          "cloudformation.amazonaws.com"
        ]
      }
    }
    ```

1. ## ๐ฌ Test the app

    - Create a new IAM User
    - Create a permission with the policy provided here `least-privileged-permissions.json`
    - Attach the policy IAM User
    - Launch the cloudformation template
      - Should launch successfully
    - Try to launch an instance with GUI/CLI it should fail

1. ## ๐งน CleanUp

    If you want to destroy all the resources created by the stack, _you can delete the cloudformationstack, permissions and IAM users from console _. Please carry out other necessary steps as maybe applicable to your needs.

## ๐ Buy me a coffee

 Buy me a coffee โ through [Paypal](https://paypal.me/valaxy), _or_ You can reach out to get more details through [here](https://youtube.com/c/valaxytechnologies/about).

### ๐ References

1. [Least Privilege Permissions](https://aws.amazon.com/blogs/security/how-to-define-least-privileged-permissions-for-actions-called-by-aws-services/)

### โน๏ธ Metadata

**Level**: 200
