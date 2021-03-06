# AWS MFA Profile
Will setup an \[mfa\] profile with an STS token. Helpful in environments where MFA is required even for development access.

# Usage

Setup AWS CLI with an access key and secret for the target MFA account. 

      > aws configure

 Install this tool globaly.

      > npm install aws-mfa-profile -g

To start the MFA process.

      > aws-mfa-profile

      Starting ...
      What is your MFA device ID? It should be in the format arn:aws:iam::ACCOUNT_ID:mfa/USERNAME.
      >

Respond to the prompt with the 'Assigned MFA device' value of your IAM profile page. Its within the 'Security Credentials' tab.

      What is your current mfa token?
      >

Next, supply a token from your MFA device.

      To use your session, use the profile mfa via --profile default-mfa (serverles is --aws-profile default-mfa)

When its complete you will see a message indicating you should use ``--profile default-mfa``. So for all of your AWS commands (or serverless.com commands) you will provide ``--profile default-mfa`` as an argument.

# Different Profiles
You can provide --profile as an argument to select a different profile to authenticate with. The MFA token will base its name off of this value, so if the profile you provide is 'foo' then the mfa credentials will be saved under 'foo-mfa'.

# Caching?
Nope, each time you run it, it will overwrite the current MFA configuration.

# .aws/credentials
This file is used to create the token and is then udpated with an additional profile when a token is succesfully added.

      [default]
      aws_access_key_id = SOME_ACCESS_KEY_ID
      aws_secret_access_key = SOME_SECRET_ACCESS_KEY


      [default-mfa]
      serial_number = arn:aws:iam::YOUR_ACCOUNT_ID:mfa/USERNAME
      aws_access_key_id = SOME_ACCESS_KEY_ID
      aws_secret_access_key = SOME_SECRET_ACCESS_KEY
      aws_session_token = SOME_BIG_LONG_SESSION_ID
      expiration = 2018-10-23T14:06:33.000Z

# Resource
https://aws.amazon.com/premiumsupport/knowledge-center/authenticate-mfa-cli/