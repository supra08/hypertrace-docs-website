---
title: Go Zipkin Exporter
weight: 3.3
template: docs
---
### Introduction
Zipkin is a distributed tracing system. It helps gather timing data needed to troubleshoot latency problems in microservice architectures.

It manages both the collection and lookup of this data. Zipkin’s design is based on the Google Dapper paper.

OpenCensus Go has support for this exporter available through package [contrib.go.opencensus.io/exporter/zipkin](https://godoc.org/contrib.go.opencensus.io/exporter/zipkin)


### Creating the exporter
To create the exporter, we'll need to:

* Create an exporter in code
* Have the Zipkin endpoint available to receive traces
 
```go
package main

import (
	"log"

	"contrib.go.opencensus.io/exporter/zipkin"
	"go.opencensus.io/trace"

	openzipkin "github.com/openzipkin/zipkin-go"
	zipkinHTTP "github.com/openzipkin/zipkin-go/reporter/http"
)

func main() {
	localEndpointURI := "192.168.1.5:5454"
	reporterURI := "http://localhost:9411/api/v2/spans"
	serviceName := "server"

	localEndpoint, err := openzipkin.NewEndpoint(serviceName, localEndpointURI)
	if err != nil {
		log.Fatalf("Failed to create Zipkin localEndpoint with URI %q error: %v", localEndpointURI, err)
	}

	reporter := zipkinHTTP.NewReporter(reporterURI)
	ze := zipkin.NewExporter(reporter, localEndpoint)

	// And now finally register it as a Trace Exporter
	trace.RegisterExporter(ze)
}
```
 
### Viewing your traces
Please visit the Hypertrace UI endpoint [http://localhost:2020](http://localhost:2020)

### Project link
You can find out more about the Zipkin project at [https://zipkin.io/](https://zipkin.io/)


<a href="https://github.com/hypertrace/hypertrace-docs-website/tree/master/src/pages/go/go-zipkin.md">
<button type="button">Edit</button></a>

***
