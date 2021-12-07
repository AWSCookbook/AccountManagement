# Setting Up Email Alerts for Root Login
## Preparation
```
You will need to have CloudTrail enabled for this. See recipe 9.3 for setup instructions.
```


## Clean up 
### Delete the SNS Topic:
```
aws sns delete-topic $TOPIC_ARN
```

### Remove the EventBridge targets from the EventBridge rule:
```
aws events remove-targets \
--rule AWSCookbook904Rule --ids 1
```

### Delete the EventBridge rule:
```
aws events delete-rule --name "AWSCookbook904Rule"
```

### Detach the AmazonSNSFullAccess policy from the role
```
aws iam detach-role-policy --role-name AWSCookbook904RuleRole \
--policy-arn arn:aws:iam::aws:policy/service-role/AmazonSNSFullAccess
```

### Delete the IAM Role: 
```
aws iam delete-role --role-name AWSCookbook904RuleRole
```

### Unset the environment variable that you created manually: 
```
unset TOPIC_ARN
```