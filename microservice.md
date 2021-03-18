
Microservice slogan: "Build it once and use it many places"
Microservice:
- Reuse
- Repurpose
- Sevice-oriented
- Scaling
- Servless

*Microservice use cases*: IoT, application service reuse, APi externalization, analytics, inventory, sales, accounting.

*Automation Tools*: Continious development -> integration -> testing -> deployment -> operations -> improvement

*Service Types*: data service, business service, translation service, edge service.

*Microservice Patterns*:
* Decomposition Patterns(Functional Use Patterns)
    * Domain Based: based on Domain Driven Design(DDD)
      DDD: Model -> Actions -> API -> Storage
    * Business Process Based: based on Business Process Domain Design(BPDD)
      BPDD: Process -> Domain(s) -> API -> wire service
    * Atomic Transaction Based
      Guarantee ACID across domains
      Designing:
      ensure the atomic service -> domains are in shared DBs ->  transactions and rollback conditions -> implement service with fast fail and rollback
* Decomposition Strategies:
    * Strangler
    * Sidecar
* Integration Patterns
    * API Gateway/Gateway: proxy, decorate, aggegate, limit access, movement buffer
      Design: define contracts, expose APIs, adhere to strict version control, implement the gateway to call your service by clients
    * Processs Aggregator: call several process together(single API call) and have a composite payload, can introduce its own processing logic, can cause long blocking calls
      Design: determine the processes, then processing rules, design a consolidated model, design an API, wire the service and implement the internal processing
    * Edge Pattern: client-specific "gateways", targets clients by focusing on isolating calls for client systems
      Design: identify the client, build contracts/models, implement contracts, maintain passivity as long as client is needed
* Data Patterns
    * Single Service, Single Database: datastore/service scale independently
    * Shared Service Database Pattern: all data domains in single DB, data distrubution is handled by DB, break data domains into schemas/tables, users don't span schemas
    * Command Query Responsibility Segregation(CQRS): multi-interface operations(write vs read), divergence from simple CRUD, increased complexity.
      When: task-based UI operations, eventual consistency is a must, event-based models and etc.
    * Asynchronous Eventing: powerful in distributed systems, cascades of events, triggering and etc...
* Operational Patterns
    * Log Aggregation: logging must be consistent/structured/shared a taxonomy, aggregation of logs, parcing of logs, correlating of logs, indexing of logs.
    * Metrics Aggregation: build high-level dashboards, detailed dashboards for services, inject events(especially deployments), trace alarms on your graphs, ensure having runbooks for all alarms
      Metrics Collection: taxonomy, system metrics, metrics shipping, dashboards
    * Tracing Patterns: re-create the call stack, should span from the edge to DB, no lost calls!
      How: standards-based appoaches, inject at the entry point, trace iD  embvedded in log messages and etc.
    * External Configuration:
      Requirements: consistent tooling, consistent naming, protect secrets, err on the side of externalization
      How: read, config, act
    * Service Discovery: central location of all services; advertise what they offer; find what is needed; consume the URI from the discovery engine, not config.
