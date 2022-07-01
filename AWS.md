# AWS

## Install AWS CLI

```sh
sudo apt install unzip
```

https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html

```sh
aws configure
```

```
Access Key: []
Secret key: []
region: us-east-1
output: json
```

## Get authenticated

```sh
aws ecr get-login-password | docker login -u AWS --password-stdin "https://$(aws sts get-caller-identity --query 'Account' --output text).dkr.ecr.us-east-1.amazonaws.com"

```
