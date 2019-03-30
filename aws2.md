aws ec2 create image --instance-id i-08ccbecd4a5dba7a7 --name new image

aws ec2 run-instances --instance-type t2.micro --subnet-id subnet-02461fe8a88f635a2  --image-id <custom imageid> --key-name test.pem
