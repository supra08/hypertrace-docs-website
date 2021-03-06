---
title: NodeJS Jaeger Exporter
weight: 4.1
template: docs
---
### Introduction
Jaeger, inspired by Dapper and OpenZipkin, is a distributed tracing system released as open source by Uber Technologies.
It is used for monitoring and troubleshooting microservices-based distributed systems, including:

* Distributed context propagation
* Distributed transaction monitoring
* Root cause analysis
* Service dependency analysis
* Performance / latency optimization

OpenCensus Node.js has support for this exporter available, distributed through NPM package [@opencensus/exporter-jaeger](https://www.npmjs.com/package/@opencensus/exporter-jaeger)

### Installing the exporter
You can install OpenCensus Jaeger Exporter by running these steps:

```bash
npm install @opencensus/core
npm install @opencensus/nodejs
npm install @opencensus/exporter-jaeger
```

### Creating the exporter
Now let's use the Jaeger exporter:
 
```javascript
const { logger } = require('@opencensus/core');
const { JaegerTraceExporter } = require('@opencensus/exporter-jaeger');
const tracing = require('@opencensus/nodejs');

// Add service name and jaeger options
const jaegerOptions = {
  serviceName: 'opencensus-exporter-jaeger',
  host: 'localhost',
  port: 6832,
  tags: [{key: 'opencensus-exporter-jeager', value: '0.0.9'}],
  bufferTimeout: 10, // time in milliseconds
  logger: logger.logger('debug')
};

const exporter = new JaegerTraceExporter(jaegerOptions);
tracing.registerExporter(exporter).start();
```
 
### Viewing your traces
Please visit the Hypertrace UI endpoint [http://localhost:2020](http://localhost:2020).

### Project link
You can find out more about the Jaeger project at [https://www.jaegertracing.io/](https://www.jaegertracing.io/)


<a href="https://github.com/hypertrace/hypertrace-docs-website/tree/master/src/pages/go/node-jaeger.md">
<button type="button">Edit</button></a>

***
