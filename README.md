EKS
- https://github.com/demopassword/EKS

Docker
- https://github.com/demopassword/Docker

vpc
- https://github.com/demopassword/VPC/tree/main/eks
- https://github.com/demopassword/VPC/tree/main/karpenter
- https://github.com/demopassword/VPC/tree/main/no-eks%26no-s3
- https://github.com/demopassword/VPC/tree/main/no-eks

### vpc flow logs iam
```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "logs:CreateLogGroup",
        "logs:CreateLogStream",
        "logs:PutLogEvents",
        "logs:DescribeLogGroups",
        "logs:DescribeLogStreams"
      ],
      "Resource": "*"
    }
  ]
}
```
```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "Service": "vpc-flow-logs.amazonaws.com"
      },
      "Action": "sts:AssumeRole"
    }
  ]
}
```

## alb s3 policy
```
{
    "Version": "2012-10-17",
    "Id": "AWSCFn-AccessLogs-Policy-20180920",
    "Statement": [
        {
            "Sid": "AlbLogs",
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::600734575887:root"
            },
            "Action": "s3:PutObject",
            "Resource": "arn:aws:s3:::bucket-aaaa213123/prefix/AWSLogs/{account_id}/*"
        }
    ]
}
```