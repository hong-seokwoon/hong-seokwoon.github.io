---
title: "React + S3 deploy"
date: 2019-12-19 15:27:00 +0900
categories: dev
---
## Workflow
1. Check existed aws configure
    - check `~/.aws/coinfig, credentials`

2. Add new profile
    - Cli command: `aws configure --profile devProfile`
    - access_key/secret_access_key[^1], region=ap-northeast-2, output=json

3. Confirm
    - Check `~/.aws/coinfig, credentials`
    - Cli command: `aws s3 ls --profile devProfile`

4. Create S3 Bucket
    - Visit S3 console[^2]
    - Bucket Name: `dev-image-album`
    - Region: `아시아 태평양(서울)`
    - Uncheck `모든 퍼블릭 액세스 차단`

5. Build project, sync
    - React project: `yarn build`
    - Check bucket name: `aws s3 ls --profile devProfile`
    - Upload files: `aws s3 sync build s3://[S3 Bucket Name] --profile devProfile`

6. Change S3 Bucket properties
    - Go to `속성 > 정적 웹 사이트 호스팅`
    - Check `이 버킷을 사용하여 웹 사이트를 호스팅합니다`
    - 인덱스 문서/오류 문서: `index.html` (*For front end routing*)
    
7. Change S3 Bucket authority
    - Go to `권한 > 버킷 정책`
    ```
    {
        "Version": "2012-10-17",
        "Statement": [
            {
                "Sid": "PublicReadForGetBucketObjects",
                "Effect": "Allow",
                "Principal": "*",
                "Action": "s3:GetObject",
                "Resource": "[S3 Bucket ARN]/*"
            }
        ]
    }
    ```
    

[^1]: [How do I find my AWS Access Key and Secret Access Key?](https://help.bittitan.com/hc/en-us/articles/115008255268-How-do-I-find-my-AWS-Access-Key-and-Secret-Access-Key-)
[^2]: [Amazon S3](https://s3.console.aws.amazon.com/s3/home?region=us-east-2#)
