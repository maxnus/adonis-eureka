# Adonis Eureka [![npm (scoped)](https://img.shields.io/npm/v/@mig-frankfurt/adonis-eureka.svg?style=flat-square)](https://www.npmjs.com/package/@mig-frankfurtadonis-eureka) [![license](https://img.shields.io/github/license/mashape/apistatus.svg?style=flat-square)](https://github.com/mig-frankfurt/adonis-eureka/blob/master/LICENSE.txt)

> :package: ServiceProvider for registering an AdonisJs Application with Netflix Eureka

Adonis Eureka is a Service Provider for registering an AdonisJs 4 application with [Eureka built by Netflix](https://github.com/Netflix/eureka). It also works with the Spring Cloud powered version of Eureka.

Built on top of [eureka-js-client](https://github.com/jquatier/eureka-js-client) for Node.js. 

**:warning: NOTE: This package is under heavy development!**

## :hand: Requirements
 - AdonisJs >= 4.0
 - Adonis Ignitor (```$ adonis install @adonisjs/ignitor```)
 
## :hammer: Setup

#### Install via adonis

```shell
$ adonis install @mig-frankfurt/adonis-eureka
```

#### Register Provider

```javascript
const providers = [
  '@mig-frankfurt/adonis-eureka/providers/EurekaProvider'
]
```

This ServiceProvider will be available under the namespace `'MigFrankfurt/Adonis/Eureka'`

#### Use hook

If not already existent, create `/start/hooks.js`

```js
const { hooks } = require('@adonisjs/ignitor')

hooks.after.httpServer(() => {
  const Eureka = use('MigFrankfurt/Adonis/Eureka')
  Eureka.start()
})
```

## :wrench: Configuration

Config will be copied during installation to `/config/eureka.js`

| Key | Env | Default | Description |
| --- | --- | --- | --- |
| eureka.defaultAccessMethod | EUREKA_DEFAULT_ACCESS_METHOD | 'byAppName' | Define the default access method for other instances. Possible: 'byAppName' or 'byVipAddr' |
|||||
| eureka.server.host | EUREKA_SERVER_HOST | 'localhost' | Hostname of the Eureka Server |
| eureka.server.port | EUREKA_SERVER_PORT | 8761 | Port of the Eureka Server  |
| eureka.server.servicePath | EUREKA_SERVER_SERVICE_PATH | '/eureka/apps/' | ServicePath of the Eureka Server|
| eureka.server.heartbeatInterval | EUREKA_SERVER_HEARTBEAT_INTERVAL | 2000 | Milliseconds to wait between heartbeats |
| eureka.server.registryFetchInterval | EUREKA_SERVER_REGISTRY_FETCH_INTERVAL | 2000 | Milliseconds to wait between registry fetches |
| eureka.server.maxRetries | EUREKA_SERVER_MAX_RETRIES | 2 | Number of times to retry all requests to eureka |
|||||
| eureka.instance.appName | EUREKA_INSTANCE_APP_NAME | 'AdonisJs Instance' | Instance name shown in Eureka |
| eureka.instance.hostname | EUREKA_INSTANCE_HOSTNAME | 'localhost' | Hostname of the instance |
| eureka.instance.ipAddr | EUREKA_INSTANCE_IP_ADDRESS | ENV('HOST') | IP address of the instance |
| eureka.instance.port | EUREKA_INSTANCE_PORT | ENV('PORT') | Port of the instance |
| eureka.instance.vipAddr | EUREKA_INSTANCE_VIP_ADDRESSS | 'adonisjs.instance' | Vip address of the instance |
| eureka.instance.dataCenterInfoName | EUREKA_INSTANCE_DATACENTER_INFO_NAME | 'MyOwn' | Datacenter Info Name of the Instance |

## :satellite: Api

#### Start Eureka

```js
const Eureka = use('MigFrankfurt/Adonis/Eureka')
Eureka.start()
```

#### Stop Eureka

```js
const Eureka = use('MigFrankfurt/Adonis/Eureka')
Eureka.stop()
```

#### Get instances by app name

```js
const Eureka = use('MigFrankfurt/Adonis/Eureka')
const instances = Eureka.getInstances('SERVICENAME') // if eureka.defaultAccessMethod === 'byAppName'
// or
const instances = Eureka.getInstancesByAppName('SERVICENAME')
```

#### Get instances by vip address

```js
const Eureka = use('MigFrankfurt/Adonis/Eureka')
const instances = Eureka.getInstances('VIPADDR') // if eureka.defaultAccessMethod === 'byVipAddr'
// or
const instances = Eureka.getInstancesByVipAddr('VIPADDR')
```

## :heavy_check_mark: Tests

:exclamation: **The tests do need a running instance of Eureka**

```js
$ npm run test
```

## :hospital: Developed by

Medical Informatics Group (MIG)\
University Hospital Frankfurt\
Theodor-Stern-Kai 7\
60590 Frankfurt\
[https://mig-frankfurt.de](https://www.mig-frankfurt.de/)

**Maintained by:** Patric Vormstein (vormstein@med.uni-frankfurt.de)

## :page_with_curl: License

MIT License

Copyright (c) 2017 Medical Informatics Group (MIG) Frankfurt

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
