# aws-nodejs-serverless
This template demonstrates how to make a simple HTTP API with Node.js running on AWS Lambda and API Gateway using Serverless Framework.


### Prerequisites

1. ```NodeJs```
2. ```NPM```


### Installation

First, add Serverless Offline to your project:

```
npm install serverless-offline --save-dev
```

Then inside your project's `serverless.yml `file add following entry to the plugins section: serverless-offline. If there is no plugin section you will need to add it to the file

Then inside your project's serverless.yml file add following entry to the plugins section: serverless-offline. If there is no plugin section you will need to add it to the file.

**Note that the "plugin" section for serverless-offline must be at root level on serverless.yml.**

It should look something like this:

```yml
plugins:
  - serverless-offline
```
You can check whether you have successfully installed the plugin by running the serverless command line:

`serverless --verbose`

the console should display ***Offline*** as one of the plugins now available in your Serverless project.

## Usage and command line options

In your project root run:

```
serverless offline or sls offline.
```

to list all the options for the plugin run:

```
sls offline --help
```

All CLI options are optional
```
--apiKey                    Defines the API key value to be used for endpoints marked as private Defaults to a random hash.
--corsAllowHeaders          Used as default Access-Control-Allow-Headers header value for responses. Delimit multiple values with commas. Default: 'accept,content-type,x-api-key'
--corsAllowOrigin           Used as default Access-Control-Allow-Origin header value for responses. Delimit multiple values with commas. Default: '*'
--corsDisallowCredentials   When provided, the default Access-Control-Allow-Credentials header value will be passed as 'false'. Default: true
--corsExposedHeaders        Used as additional Access-Control-Exposed-Headers header value for responses. Delimit multiple values with commas. Default: 'WWW-Authenticate,Server-Authorization'
--disableCookieValidation   Used to disable cookie-validation on hapi.js-server
--disableScheduledEvents    Disables all scheduled events. Overrides configurations in serverless.yml.
--dockerHost                The host name of Docker. Default: localhost
--dockerHostServicePath     Defines service path which is used by SLS running inside Docker container
--dockerNetwork             The network that the Docker container will connect to
--dockerReadOnly            Marks if the docker code layer should be read only. Default: true
--enforceSecureCookies      Enforce secure cookies
--hideStackTraces           Hide the stack trace on lambda failure. Default: false
--host                  -o  Host name to listen on. Default: localhost
--httpPort                  Http port to listen on. Default: 3000
--httpsProtocol         -H  To enable HTTPS, specify directory (relative to your cwd, typically your project dir) for both cert.pem and key.pem files
--ignoreJWTSignature        When using HttpApi with a JWT authorizer, don't check the signature of the JWT token. This should only be used for local development.
--lambdaPort                Lambda http port to listen on. Default: 3002
--layersDir                 The directory layers should be stored in. Default: ${codeDir}/.serverless-offline/layers'
--localEnvironment          Copy local environment variables. Default: false
--noAuth                    Turns off all authorizers
--noPrependStageInUrl       Don't prepend http routes with the stage.
--noStripTrailingSlashInUrl Don't strip trailing slash from http routes.
--noTimeout             -t  Disables the timeout feature.
--prefix                -p  Adds a prefix to every path, to send your requests to http://localhost:3000/[prefix]/[your_path] instead. Default: ''
--printOutput               Turns on logging of your lambda outputs in the terminal.
--reloadHandler             Reloads handler with each request.
--resourceRoutes            Turns on loading of your HTTP proxy settings from serverless.yml
--useChildProcesses         Run handlers in a child process
--useDocker                 Run handlers in a docker container.
--useInProcess              Run handlers in the same process as 'serverless-offline'.
--webSocketHardTimeout      Set WebSocket hard timeout in seconds to reproduce AWS limits (https://docs.aws.amazon.com/apigateway/latest/developerguide/limits.html#apigateway-execution-service-websocket-limits-table). Default: 7200 (2 hours)
--webSocketIdleTimeout      Set WebSocket idle timeout in seconds to reproduce AWS limits (https://docs.aws.amazon.com/apigateway/latest/developerguide/limits.html#apigateway-execution-service-websocket-limits-table). Default: 600 (10 minutes)
--websocketPort             WebSocket port to listen on. Default: 3001
```

Any of the CLI options can be added to your serverless.yml. For example:

```yml
custom:
  serverless-offline:
    httpsProtocol: 'dev-certs'
    httpPort: 4000
      foo: 'bar'
```
Options passed on the command line override YAML options.

By default you can send your requests to `http://localhost:3000/`. Please note that:

You'll need to restart the plugin if you modify your serverless.yml or any of the default velocity template files.
When no Content-Type header is set on a request, API Gateway defaults to application/json, and so does the plugin. But if you send an application/x-www-form-urlencoded or a multipart/form-data body with an application/json (or no) Content-Type, API Gateway won't parse your data (you'll get the ugly raw as input), whereas the plugin will answer 400 (malformed JSON). Please consider explicitly setting your requests' Content-Type and using separate templates.


### Local development

You can invoke your function locally by using the following command:

```
serverless invoke local --function hello
```

Which should result in response similar to the following:

```
{
    "statusCode": 200,
    "body": "{\n  \"message\": \"Go Serverless v3.0! Your function executed successfully!\",\n  \"input\": \"\"\n}"
}

```
Alternatively, it is also possible to emulate API Gateway and Lambda locally by using serverless-offline plugin. In order to do that, execute the following command:

```
serverless plugin install -n serverless-offline
```

It will add the serverless-offline plugin to devDependencies in package.json file as well as will add it to plugins in serverless.yml.

After installation, you can start local emulation with:
```
serverless offline
```

you can also try 
```
sls offline
```