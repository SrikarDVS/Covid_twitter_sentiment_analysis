# Covid_twitter_sentiment_analysis

# This guide assumes you are on a Linux based OS

# Table of Contents
  * [Pre-Requisites](#pre-requisites)
  * Running the application (Ensure you have the prerequisites installed)
    + [A. Setting up AWS account and getting your ssh key](#a-setting-up-aws-account-and-getting-your-ssh-key)
    + [B. Setting up Terraform](#b-setting-up-terraform)
    + [C. Setting up Twitter API](#c-setting-up-twitter-api)
    + [D. Running Terraform](#d-running-terraform)
    + [E. Databricks](#e-databricks)
  * [Variables in the tfvars file](#variables-in-the-tfvars-file)
  * [Variables in the twitter-analytics.py file](#variables-in-the-twitter-analyticspy-file)
  * [Variables in the tweets.ipynb file](#variables-in-the-tweetsipynb-file)

## Pre-Requisites
1. [AWS account (Free tier)](https://aws.amazon.com/premiumsupport/knowledge-center/create-and-activate-aws-account/)
2. [Databricks ID (Community Edition)](https://community.cloud.databricks.com/login.html)
3. [Access to twitter API](https://developer.twitter.com/en/docs/twitter-api/getting-started/getting-access-to-the-twitter-api)
4. [Terraform on you local machine](https://learn.hashicorp.com/tutorials/terraform/install-cli)
5. A text editor to use to create terraform config files

## Running the application (Ensure you have the prerequisites installed)

### A. Setting up AWS account and getting your ssh key
  1. First ensure you have created an aws account by following the link given in the prerequisite section.
  2. Ideally you have already set up a user with [programmatic permissions](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users_create.html).
  3. The next step is to create a key pair. [These are the steps for creating a key pair.](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-key-pairs.html)
  4. Once you create the key pair you will be prompted to download the ssh private key, which you need to save on your local machine, this will be useful later.
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
  5. Open the "terraform.tfvars" file and enter the required variables.The details of the variables can be found [here.](#variables-in-the-tfvars-file)
  7. Move the private key downloaded earlier into this directory.
  8. Change the ssh key permissions using the chmod 400 command ( chmod 400 "Keyname" )
  ```console
user@machine:~/Desktop/$ chmod 400 <keyname>
```
  
### C. Setting up Twitter API
  1. Follow the steps for getting access to the twitter api given in the prerequisites, this will allow you to create apps and access keys.
  2. Create a twitter standalone app and from the keys section get the consumer and access token keys. ( Each will have a key and a secret key, so there will be 4 keys in total )
  3. Open the twitter_analytics.py file and fill in those keys where required, along with aws credentials for the data stream. Details of the variables are [here]((#variables-in-the-twitter-analyticspy-file)
  
### D. Running Terraform
  1. Open a terminal in the terraform_config folder and run the command  
```console
user@machine:~/Desktop/Covid_twitter_sentiment_analysis/$ terraform init 
```
  2. Then run terraform apply and type "yes" when required.
```console
user@machine:~/Desktop/Covid_twitter_sentiment_analysis/$ terraform apply
``` 
  3. This process will take a couple of minutes, but the output should be the twitter stream running and showing you individual tweets having the keyword covid19.
  
### E. Databricks
  1. Make a databricks community account in the link given in the [pre-requisites]((#pre-requisites)
  2. Import the notebook given in the repo into databricks by following the guide [here.](https://docs.databricks.com/notebooks/notebooks-manage.html#import-a-notebook)
  3. In the notebook the cells are labelled in accordance with what they do, there are 2 labels, ingestion and processing. This label is basically the work "ingesiton" or "processing" commented at the beginning of the cell.
  4. Initially enter the variables required, details are found [here.](#variables-in-the-tweetsipynb-file)
  5. Once you have given the details, run all the cells which are marked as ingestion, and then wait for 15 minutes. This will give some time for the program to fetch tweets and store them in the spark dataframe.
  6. Once you have let the ingestion cells run, you can run the processing cells, these will clean the data, process it and visualize the processed data


### Variables in the tfvars file

1. **AWS access key**: This is your amazon aws access key for the user profile you are using, instructions on how to get it are given [here.](https://docs.aws.amazon.com/general/latest/gr/aws-sec-cred-types.html)
2. **AWS secret key**: This is the secret key tied to the user profile, you can learn how to find it [here.](https://docs.aws.amazon.com/general/latest/gr/aws-sec-cred-types.html)
3. **VPC region**: This is where you specify which region you want your aws vpc to be created, you can find a list of regions [here.](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Concepts.RegionsAndAvailabilityZones.html)
4. **VPC cider block**: This is the block you are allocating to your vpc to make further divisions on, more details on vpc and subnets are [here.](https://docs.aws.amazon.com/vpc/latest/userguide/working-with-vpcs.html)
5. **VPC subnet ip**: This is the ip you are giving to the public subnet, from your cider block.
6. **AMI name**: You can get this from [here](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/finding-an-ami.html)
7. **ec2 name**: This is the name you give to your ec2 instance.
8. **sshkeyname**: This is the name of the ssh key pair you created earlier.
9. **VPC private subnet ip**: This is the ip you are giving to your private subnet.
10. **VPC public subnet access ip range**: This is used to restrict access to the public ip of the subnet from a given range of ip addresses, you can give 0.0.0.0/0 to permit anyone to access.


### Variables in the twitter-analytics.py file

1. **Consumer key**: This is the consumer key given by the twitter api and can be found on the console of the app you made.
2. **Consumer secret key**: This is the consumer key given by the twitter api and can be found on the console of the app you made.
3. **Access token**: This is the consumer key given by the twitter api and can be found on the console of the app you made.
4. **Secret Access token**: This is the consumer key given by the twitter api and can be found on the console of the app you made.
5. **region name**: This is the region you gave in the variables file earler.
6. **aws secret key id**: Same as the one in the variables file.
7. **aws secret access key**: Same as the one in the variables file.

### Variables in the tweets.ipynb file

1. **AWS access key id**: Same as in variables file.
2. **AWS secret key id**: Same as in variables file.
3. **AWS region**: Same as in variables file.
