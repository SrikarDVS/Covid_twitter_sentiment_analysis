# Covid_twitter_sentiment_analysis


## Pre-Requisites
1. AWS account (Free tier)
2. Databricks ID (Community Edition)
3. Access to twitter API
4. Terraform on you local machine
5. A text editor to use to create terraform config files

## Running the application (Ensure you have the prerequisites installed)


### A. Setting up Terraform
  1. First clone the repo to you local machine.
  ```console
user@machine:~/Desktop/$ gh repo clone SrikarDVS/Covid_twitter_sentiment_analysis
```
  2. Navigate to the terraform_config directory
```console
user@machine:~/Desktop/$ cd Covid_twitter_sentiment_analysis
```
  3. In this directory you will find the files "vpc.tf", "variables.tf" and "terraform.tfvars"
  4. Open the "terraform.tfvars" file and enter the variables required. ( Get the ami details using this https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/finding-an-ami.html )
  5. Download the private ssh key with the same name as given in the "tfvars" file, place this key in the terraform_config directory
  6. Change the ssh key permissions using the chmod 400 command ( chmod 400 "Keyname" )
  
### B. Setting up Twitter API
  1. Create a twitter standalone app and from the keys section get the consumer and access token keys. ( 4 keys in total, 2 from each )
  2. Open the twitter_analytics.py file and fill in those keys where required along with aws credentials for the data stream.
  
### C. Running Terraform
  1. Open a terminal in the terraform_config folder and run the command  
```console
user@machine:~/Desktop/Covid_twitter_sentiment_analysis/$ terraform init 
```
  2. Then run terraform apply and type "yes" when required.
```console
user@machine:~/Desktop/Covid_twitter_sentiment_analysis/$ terraform apply
``` 
  3. This process will take around 2 mins, but the output should be the twitter stream running and showing you individual tweets having the keyword covid19.
  
### D. Databricks
  1. Open databricks and import the python notebook from the repo
  2. Run all the cells to ingest data and wait to accumulate a few samples, then run the cells for processing and cleaning the data and finally the cells to visulaize the data
