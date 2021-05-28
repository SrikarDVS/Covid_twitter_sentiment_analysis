# Covid_twitter_sentiment_analysis

## Pre-Requisites
1. AWS account (Free tier)
2. Databricks ID (Community Edition)
3. Access to twitter API
4. Terraform on you local machine
5. A text editor to use to create terraform config files

## Running the application (Ensure you have the prerequisites installed)
A. Setting up terraform
1. First clone the repo to you local machine.
2. Navigate to the terraform_config directory
3. In this directory you will find the files "vpc.tf", "variables.tf" and "terraform.tfvars"
4. Open the "terraform.tfvars" file and enter the variables required. ( Get the ami details using this https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/finding-an-ami.html )
5. Download the private ssh key with the same name as given in the "tfvars" file, place this key in the terraform_config directory
6. Change the ssh key permissions using the chmod 400 command ( chmod 400 "Keyname" )
7. Open the python script called twitter_analytics.py 
