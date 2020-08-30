
AWS KMS key:
arn:aws:kms:us-east-2:893546316829:key/6e0cb341-d368-4aba-820e-d3d7415e6fa1



Set-Up Commands:

1. brew install kube-aws
2. aws configure
	- follow the prompt with your aws account's access key and secret key
	- input the aws region you are trying to access with your instances
	- use the text method
3. aws kms --region=us-east-2 create-key --description "kue-aws assets"
	- create aws kms key for your account hosted in the region of your instances 
	use the "KeyMetadata.Arn" string to identify your KMS key in the init setup
4. External DNS
	- Select a DNS hostname where the cluster API will be accessible. Typically this hostname is available over the internet ("external"), so end users can connect from different networks. This hostname will be used to provision the TLS certificate for the API server, which encrypts traffic between your users and the API. Optionally, you can provide the certificates yourself, which is recommended for production clusters.
	- the cluster will expose the TLS-secured API on an internet-facing ELB. kube-aws can automatically create an ALIAS record for the ELB in an existing Route 53 hosted zone 
		- "--hosted-zone-id" flag to specify
	- omit --hosted-zone-id by specifying the --no-record-set flag
	- find the public DNS name of the ELB after the cluster is created by invoking kube-aws status.
5. S3 bucket
	-  aws s3api create-bucket --bucket my-bucket --region us-east-2 --create-bucket-configuration LocationConstraint=us-east-2

