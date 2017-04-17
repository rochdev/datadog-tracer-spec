# [WIP] Datadog Tracer Specification

OpenTracing propagation specification for Datadog distributed tracing. This specification was created to ensure that distributed tracing works properly across the different implementations in any programming language.

## Propagation

### Text Map

Text map propagation uses the following keys:

* **dd-tracer-traceid**
* **dd-tracer-spanid**
* **dd-tracer-sampled**
* **dd-baggage-{key}**

### HTTP Headers

Same as text map. Additionally, keys and values should be suitable according to [RFC 7230](https://tools.ietf.org/html/rfc7230#section-3.2.4).

### Binary

Binary propagation is done using [Protocol Buffers Version 3](https://developers.google.com/protocol-buffers/docs/reference/proto3-spec) in the following format:

```protobuf
syntax = "proto3";

message TracerState {
  string trace_id = 1;
  string span_id = 2;
  bool   sampled = 3;
  map<string, string> baggage = 4;
}
```
