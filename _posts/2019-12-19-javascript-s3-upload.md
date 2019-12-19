---
title: "Javascript S3 File Upload"
date: 2019-12-19 16:28:00 +0900
categories: dev
---
## JS
```javascript
    import AWS from 'aws-sdk';
    
    AWS.config.update(config.aws_remote_config);
    
    const s3 = new AWS.S3();
    const filename = "Small_size.vcf";
    const param = {
      'Bucket': '3billion-portal-data',
      'Key': 'vcf/' + filename,
      'ACL':'public-read',
      'Body':fs.createReadStream('./data/' + filename),
    };
    
    s3.upload(param, (err, data) => {
      log(err);
      log(data);
    });
```

## config.js
```json
module.exports = {
  aws_table_name: 'YOUR_TABLE_NAME',
  aws_local_config: {
    region: 'ap-northeast-2',
    endpoint: 'http://localhost:8000'
  },
  aws_remote_config: {
    region: 'ap-northeast-2'
  }
};
```
