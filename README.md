# Instructions to deploy

`aws cloudformation create-stack --stack-name udacity-webapp --template-body file://./networkInfrastructure.yaml --parameters file://./networkParameters.json --region=us-west-2 --capabilities CAPABILITY_IA`
`aws cloudformation create-stack --stack-name udacity-webapp-server --template-body file://./serverInfrastructure.yaml --parameters file://./serverParameters.json --region=us-west-2 --capabilities CAPABILITY_IAM`

# Current deployment
