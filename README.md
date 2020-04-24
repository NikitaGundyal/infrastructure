# infrastructure

AWS Infrastructure As Code
Infrastructure Setup includes:

1. VPC
2. Three Public Subnets in different availability zones in the same region
3. Internet Gateway with AttachInternetGateway resource
4. A public routetable which has the above 3 subnets associated with it
5. A public route in the above route table with destination CIDR block of 0.0.0.0/0 and internet gateway attached

Cloudformation Template
networking.json is the cloudformation template which builds the network stack

Commands to execute:
1. To create stack
aws cloudformation create-stack --stack-name <>

2. To delete stack
aws cloudformation delete-stack --stack-name <>

Steps to upload SSL Certificate to ACM
1. Navigate to the folder where you have downloaded the SSL certificate from Namecheap.
2. $openssl x509 -in {ca-bundle} -out certificatechain.pem
3. $openssl x509 -in  {.crt} -out {any-name}.pem
4. $vi product.key #paste your private key 
5. $ aws acm import-certificate --certificate fileb://{any-name}.pem --privatekey fileb://product.key --certificate-chain fileb://certificatechain.pem --profile {aws profile}
