---
title: Architecture
excerpt: >-
  Libris is a Unibit theme created for project documentations. You can use it
  for your project.
template: docs
---
# Hypertrace Architecture

Hypertrace is a highly scalable distributed tracing and observability platform designed to ingest and analyze large volumes of production trace data. OpenTelemetry-based agents collect and send observability data directly from applications to Hypertrace for analysis. Data visualizations, reports, and dashboards are available in a web-based console to assist in monitoring cloud-native applications and resolving application and service performance problems.

Hypertrace has fairly complex architecture than most of the Distributed Tracing platforms out there because og immense functionality it provides as a platform. 

Let's take a look at Hypertrace architecture and undestand each component in details.


| ![space-1.jpg](static/architecture.png) | 
|:--:| 
| *Hypertrace Architecture* |

### 1. Collect traces in multiple formats:
One important requirement to start working with hypertrace is, your application must be instrumented before it can send tracing and monitoring data to any currently supported backend including OpenTracing, OpenCensus, Jaeger and zipkin. 

Hypertrace is able to collect traces from any of the formats these platforms support. Hypertrace supports OpenTracing standards out of the box so we can expect it to suppport all applications using OpenTracing API with a backwards compatibility to Zipkin. 

We will be adding support to OpenTelemetry collector soon which will make Hypertrace more future proof and robust as a platform.

### 2. Storage layer:
Storage layer uses OLAP currently which is in real-time store. It is possible to change this to any relational DB like postgres or even Cassandra or Elasticsearch. Going ahead, we are trying to make this plug and play transition as simple as possible. Currently we are relying on pinot. 

### 3. Processing layer:
Processing layer here uses Flink to read from and write to kafka topics. currently we are using flink local mode but we are looking into providing other modes according to scale. 

### 4. Customizable Enrichers and Views: 
Trace enricher is what basically provides a way to incorporate business logic in our current setup. There are variety of customizations you can add using trace enricher by writing some java code. Customizations can include protocols for various backends or some custom metrics. It helps us to get most out of out span data.

### 5. Flexible query layer + GraphQL
When we look into classic REST API calls for fetching trace data we can get all the information at ones or no information at all. REST API's do not provide us selectability or ability to limit the scope. GraphQL solves this problem.  The query layer which involves this different services which work together is flexible and scalable. 

### 6. UI
Hypertrace UI is based on custom framework written by hypertrace team which we call Hyperdash. Hypertrace UI uses Angular and is open source with some parts under source available licence. It's a beautiful UI with bunch of features and functionalities out of the box which will help you troubleshoot issues with your application and find performance issues. You can check out this [page](docs/UI.md) for more information about UI and features. 


***

Here are the articles in this section: