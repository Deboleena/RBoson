# RBoson
An R library for distributed computing using AWS.

## Installation:
Install AWS CLI from a console running: pip install awscli --upgrade --user\
Install RBoson from R:\
install.packages("devtools")\
library(devtools)\
install_github("Deboleena/RBoson")\
require(RBoson)

## One-time configuration
AWSConfigure(\
  aws.access.key.id = '****',\
  aws.secret.access.key = '****'\
)

## Execution
\# Setup \#\
BosonSetup (\
  service.role.arn = "arn:aws:iam::757968107665:role/BosonBatch",\
  subnets = c("subnet-1a69d77d","subnet-4da19315","subnet-abfc2ce2"),\
  security.group.ids = "sg-ddd562a7"\
)\
\
\# Execution \#\
\# Step 1: Define tasks\
BosonTask = function (x) {\
	return ( x * x )\
}\
BosonParams = list()\
for (x in 1:100) {\
    BosonParams[[x]] = list(x = x)\
}\
\
\# Step 2: Bootstrapping\
out = SubmitBosonTasks (\
  X = BosonParams,\
  FUN = BosonTask,\
  njobs = 10,\
  s3.bucket = 's3://boson-base/',\
  blocking.call = TRUE\
)\
print(out)\
\
\# Step 3: Cleanup\
BatchCleanup(batch.id = 1, s3.bucket = 's3://boson-base/')

## Cleanup
BosonCleanup()