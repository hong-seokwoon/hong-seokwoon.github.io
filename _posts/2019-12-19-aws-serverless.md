---
title: "AWS + Serverless deploy"
date: 2019-12-19 15:07:00 +0900
categories: dev
---
## Workflow
1. Set up the Serverless Framework[^1]
2. Deploy by AWS profile[^2]
    - `serverless deploy --aws-profile devProfile`

## Issue
1. `sls offline start` Access denied => serverlsss.yml
    ```yml
    plugins:
      - serverless-offline
      #- serverless-bundle # Package our functions with Webpack
      #- serverless-dotenv-plugin # Load .env as environment variables
    ```
    
2. Error `module exports is undefined` [^3]
    - Error
        ```javascript
        module.exports.handler = serverless(app)    
        ```
    - OK  
        ```javascript
        module.exports {
            handler: serverless(app);
        }
        ```

3. AWS Profile Error
    - Error
        ```
        sls offline start --aws-profile devProfile
        ```
    - OK
        ```
        export AWS_PROFILE=devProfile && export AWS_REGION=ap-northeast-2
        
        sls offline start
        ```

[^1]: https://serverless-stack.com/chapters/setup-the-serverless-framework.html
[^2]: https://serverless.com/framework/docs/providers/aws/guide/credentials/
[^3]: https://medium.com/free-code-camp/node-js-module-exports-vs-exports-ec7e254d63ac
