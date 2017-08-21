# RBoson
An R library for distributed computing using AWS.

## Installation:
Install AWS CLI from a console running: pip install awscli --upgrade --user\
Install RBoson from R:\
install.packages("devtools")\
library(devtools)\
install_github("Deboleena/RBoson")

## One-time configuration
AWSConfigure(\
  aws.access.key.id = '****',\
  aws.secret.access.key = '****'\
)

## Execution