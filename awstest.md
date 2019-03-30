aws configure

aws ec2 create-vpc --cidr-block 10.0.0.0/16
     "VpcId": "vpc-0ce558be57644f34f"
     "CidrBlock": "10.0.0.0/16"

aws ec2 create-subnet  --cidr-block 10.0.0.0/24 --vpc-id vpc-0ce558be57644f34f
    "SubnetId": "subnet-02461fe8a88f635a2"

aws ec2 create-internet-gateway
    "InternetGatewayId": "igw-0a58d7fa26b57bbc1"

aws ec2 attach-internet-gateway --vpc-id vpc-0ce558be57644f34f --internet-gateway-id igw-0a58d7fa26b57bbc1
    "RouteTableId": "rtb-05f1d358a05026254"

aws ec2 create-route --route-table-id rtb-05f1d358a05026254 --destination-cidr-block 0.0.0.0/0 --gateway-id igw-0a58d7fa26b57bbc1

aws ec2 associate-route-table  --subnet-id subnet-02461fe8a88f635a2 --route-table-id rtb-05f1d358a05026254
    "AssociationId": "rtbassoc-01c03f65a71e57dbb"
    
aws ec2 run-instances --instance-type t2.micro --subnet-id subnet-02461fe8a88f635a2  --image-id ami-08692d171e3cf02d6 --key-name test.pem
    "InstanceId": "i-08ccbecd4a5dba7a7"

aws ec2 allocate-address
    "PublicIp": "54.68.23.135"
     "AllocationId": eipalloc-098ef9f1c7fbbb25b

aws ec2 associate-address --public-ip 54.68.23.135 --instance-id i-08ccbecd4a5dba7a7
    "AssociationId": "eipassoc-09c40afc7501346e2"
# login into machine
 ssh -i "test.pem" ubuntu@54.68.23.135

 



