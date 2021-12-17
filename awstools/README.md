# Requirements

- AWSTools has been written against Python 3.  I haven't tried (nor will support)
Python 2.
- AWSTools requires the following 3rd party APIs, which must be installed if you
don't have them already.

``` 
pip3 install boto3
```

- The environment should contain a valid AWS profile.  If you have AWS
Multi-Factor Authentication enabled for your account, you will need to use the
AWS-STS service to get a temporary session credential *before* using these
tools.
- TBD - The AWS_DEFAULT_KEY variable must be set and point to a valid PEM.
- TBD If not set, when tools need a PEM key, they will try all those in
  ~/.aws/keys until one works.


# Help

Each tool contains its own help, accessible with `--help`.  
