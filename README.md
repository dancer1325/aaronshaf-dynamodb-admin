# dynamodb-admin

* [![npm](https://img.shields.io/npm/v/dynamodb-admin.svg)](https://www.npmjs.com/package/dynamodb-admin)
* GUI -- for --
  * [DynamoDB Local](https://aws.amazon.com/blogs/aws/dynamodb-local-for-desktop-development/)
  * [dynalite](https://github.com/mhart/dynalite)
  *  [localstack](https://github.com/localstack/localstack)

## ways to use

### -- as -- globally installed app

```bash
# 1. install
npm install -g dynamodb-admin

# 2. run it
# 2.1 all default options
dynamodb-admin --dynamo-endpoint=http://localhost:8000
```

* ways to pass options
  * -- via -- CL options
    * _Example:_ `dynamodb-admin --dynamo-endpoint=http://localhost:8000 --ALLOWEDOPTIONS`
    * `ALLOWEDOPTIONS`
      - `--open` / `-o`
        - opens DIRECTLY server URL | your default browser
      - `--port PORT` / `-p PORT`
        - port | run on
          - by default, 8001
      - `--host HOST` / `-h HOST`
        - host | run on
          - by default, localhost
      - `--dynamo-endpoint`
        - DynamoDB endpoint | connect to
          - by default, http://localhost:8000
      - `--skip-default-credentials`
        - ⚠️skip setting default credentials & region⚠️
          - by default,
            - accessKeyId/secretAccessKey == key/secret
            - region == us-east-1
          - requirements
            - provide credentials -- via -- [other way](https://docs.aws.amazon.com/sdk-for-javascript/v3/developer-guide/setting-credentials-node.html) 
  * -- via -- environment variables
    * `HOST`
    * `PORT`
    * `DYNAMO_ENDPOINT`
    * `AWS_REGION`
    * `AWS_ACCESS_KEY_ID`
    * `AWS_SECRET_ACCESS_KEY`
    * _Example:_ `AWS_REGION=eu-west-1 AWS_ACCESS_KEY_ID=local AWS_SECRET_ACCESS_KEY=local dynamodb-admin`

### -- as a -- library | your project

* requirements
  * AWS SDK v3
    * if you use AWS SDK v2 -> use dynamodb-admin v4

```js
import { DynamoDBClient } from '@aws-sdk/client-dynamodb';
import { createServer } from 'dynamodb-admin';

const dynamoDbClient = new DynamoDBClient();

const app = createServer({ dynamoDbClient });

const host = 'localhost';
const port = 8001;
const server = app.listen(port, host);
server.on('listening', () => {
  const address = server.address();
  console.log(`  listening on http://${address.address}:${address.port}`);
});
```

### -- as -- container

* container images
  * ONLY [dynamodb-admin](Dockerfile) 
    * published | [DockerHub](https://hub.docker.com/r/aaronshaf/dynamodb-admin/)
  * dynamodb-admin + dynamodb
    * published | [DockerHub](https://github.com/instructure/dynamo-local-admin-docker)

## Development

* steps
  * `npm run build` OR `npm run build:watch`
  * `DYNAMO_ENDPOINT=http://localhost:8000 npm run start` 
    * start dynamodb-admin

## See also

* [Camin McCluskey's Quick Start Guide](https://medium.com/swlh/a-gui-for-local-dynamodb-dynamodb-admin-b16998323f8e)
