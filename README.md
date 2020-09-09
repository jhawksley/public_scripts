# public_scripts

This folder is a little collection of scripts I've written over the years.  I'll be adding and uploading them gradually, so check back periodically to see what's new.

There is no support or guarantees with them:  you use them at your own risk.

They may be Bash, Ruby or Python, depending on what mood I was in that day.

# Index

### aws-sts

Retrieve and format an AWS STS Credential for the shell environment.

This script uses your CLI [AWS credentials](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-files.html?shortFooter=true) to get an [AWS Security Token Service](https://docs.aws.amazon.com/STS/latest/APIReference/welcome.html) temporary credential.  

This is useful for those of us with Multi-Factor Authentication enabled on our accounts.  If MFA is enabled, your Access Key and Secret Key are used in conjunction with your current MFA token to generate a temporary Access Key, Secret Key and Session Token.  You can set these in the environment and then use the CLI as normal.  

#### Requirements

Must be in path:

* jq
* aws v3+

#### Usage

1. Store your MFA serial (usually of the form `arn:aws:iam::YOUR_ACCOUNT:mfa/YOUR_USERNAME`) in your current profile with:
```bash
aws configure set mfa_serial arn:aws:iam::YOUR_ACCOUNT:mfa/YOUR_USERNAME
```
2. Use your MFA device to get the current token, and run the script to see what it's going to do:
```bash
aws-sts CURRENT_TOKEN_SERIAL
```
This will obtain an STS token for you and spit out the right shell code to set up the temporary credential:
```bash
unset AWS_DEFAULT_REGION AWS_SESSION_TOKEN AWS_SECRET_ACCESS_KEY AWS_ACCESS_KEY_ID;
export AWS_DEFAULT_REGION=eu-west-1;
export AWS_SESSION_TOKEN="SESSION_TOKEN_REDACTED";
export AWS_ACCESS_KEY_ID="ACCESS_KEY_REDACTED";
export AWS_SECRET_ACCESS_KEY="SECRET_KEY_REDACTED"
```
3. Run the code again and have the shell run the result:
```bash
eval $(aws-sts CURRENT_TOKEN_SERIAL)
```

