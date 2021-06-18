# Covid_twitter_sentiment_analysis

# This guide assumes you are on a Linux based OS

## Pre-Requisites
1. [AWS account (Free tier)](https://aws.amazon.com/premiumsupport/knowledge-center/create-and-activate-aws-account/)
2. [Databricks ID (Community Edition)](https://community.cloud.databricks.com/login.html)
3. [Access to twitter API](https://developer.twitter.com/en)
4. [Terraform on you local machine](https://learn.hashicorp.com/tutorials/terraform/install-cli)
5. A text editor to use to create terraform config files

## Running the application (Ensure you have the prerequisites installed)

### A. Setting up AWS account and getting your ssh key
  1. First ensure you have created an aws account by following the link given in the prerequisite section.
  2. Ideally you have already set up a user with programmatic permissions
### B. Setting up Terraform
  1. Install terrform by following the steps given in the link in the prerequisites.
  2. Then clone the repo to you local machine.
  ```console
user@machine:~/Desktop/$ gh repo clone SrikarDVS/Covid_twitter_sentiment_analysis
```
  3. Navigate to the terraform_config directory
```console
user@machine:~/Desktop/$ cd Covid_twitter_sentiment_analysis
```
  4. In this directory you will find the files "vpc.tf", "variables.tf","terraform.tfvars","twitter_analytics.py","Tweets.ipynb"
  5. Open the "terraform.tfvars" file and enter the required variables. [The details of the variables can be found here.](# Variables in the "tfvars" file)
  7. Download the private ssh key with the same name as given in the "tfvars" file, place this key in the terraform_config directory
  8. Change the ssh key permissions using the chmod 400 command ( chmod 400 "Keyname" )
  
### C. Setting up Twitter API
  1. Create a twitter standalone app and from the keys section get the consumer and access token keys. ( 4 keys in total, 2 from each )
  2. Open the twitter_analytics.py file and fill in those keys where required along with aws credentials for the data stream.
  
### D. Running Terraform
  1. Open a terminal in the terraform_config folder and run the command  
```console
user@machine:~/Desktop/Covid_twitter_sentiment_analysis/$ terraform init 
```
  2. Then run terraform apply and type "yes" when required.
```console
user@machine:~/Desktop/Covid_twitter_sentiment_analysis/$ terraform apply
``` 
  3. This process will take around 2 mins, but the output should be the twitter stream running and showing you individual tweets having the keyword covid19.
  
### E. Databricks
  1. Open databricks and import the python notebook from the repo
  2. Run all the cells to ingest data and wait to accumulate a few samples, then run the cells for processing and cleaning the data and finally the cells to visulaize the data


### Variables in the "tfvars" file

1.
2.
3.

