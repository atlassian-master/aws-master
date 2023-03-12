#####  Goal:

   Get the public IP of the EC2 instance. 
   
##### Youtube Video:

https://youtu.be/beDqF1fUXZM


##### Background:

   - By default, public IP will be changed after restarting EC2 instance, unless an Elastic Public IP is associated to the EC2 networking.

   - The session is to help to run: 
       1. Retart the EC2 instance
       2. Get the new IP address and print it out for other use

##### Skills Used:

  - AWS CLI


##### Implementation:

  - Download AWS CLI and run 
  ```
  aws configure
  ```

  - Add a bash scripting like the following content:


```
 #!/bin/bash

aws ec2 stop-instances --instance-ids i-0fce92d54b4121d53
sleep 60
aws ec2 start-instances --instance-ids i-0fce92d54b4121d53
sleep 30
aws ec2 describe-instances --instance-ids i-0fce92d54b4121d53 | grep PublicIpAddress | awk -F ":" '{print $2}' | sed 's/[",]//g'
```

If you just only want to get the IP without restarting the EC2 instance, just have the script like this is good enough.

```
 #!/bin/bash
aws ec2 describe-instances --instance-ids i-0fce92d54b4121d53 | grep PublicIpAddress | awk -F ":" '{print $2}' | sed 's/[",]//g'
```

  - Make the script executble: chmox + get_ip.sh
 
  - Run the script: ./get_ip.sh
