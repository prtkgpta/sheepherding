# sheepherding
## Summary
A collection of scripts designed to be run periodically through on AWS Lambda to manage an AWS deployment. These are simple scipts, written in python, to provide some inspiration on what can be achieved without relying on third party reporting tools or dedicated reporting instances. Many of these scripts cost fractions of cents to run! A script run once a week, taking 60s to execute and using the minimum ammount of ram will cost less than $0.05 a year!
# Current Scripts
* ```reserved_instance_report.py``` - This provides a report of all reserved instances and those that will shortly expire to ensure that cost savings are maintained.
* ```photographer.py``` - Backup script to take images of instances and snapshots of volumes. Configured via an ConfigParser config file, stored in an S3 bucket.

# Installation Instructions

All of the scripts in the scripts directory are intended to be installed in a very similar way:
* Create an IAM role with a policy that allows access to the components used in the script, example policys are provided in the iam_policy_examples directory.
* Create a scheduled event to initiate the lambda function as frequently as required, "cron(0 0 ? * 1 *)" will run it weekly at midnight on Sunday for example.
* Either:
  * Copy and paste the script into the code section, updating any of the customisations defined at the beginning of the handler function (which is always lambda_function.lambda_handler)
  * Zip and upload the .py file and specify the handler as file_name.lambda_handler
* Some of the scripts take longer to run than others and will require more ram, so you may need to increase the limits if you have a very large infrastructure.
