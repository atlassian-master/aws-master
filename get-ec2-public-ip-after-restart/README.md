


```
 #!/bin/bash

#aws ec2 stop-instances --instance-ids i-0fce92d54b4121d53
#sleep 60
#aws ec2 start-instances --instance-ids i-0fce92d54b4121d53
#sleep 30
aws ec2 describe-instances --instance-ids i-0fce92d54b4121d53 | grep PublicIpAddress | awk -F ":" '{print $2}' | sed 's/[",]//g'
```
