# Event-Driven Architecture

## Done it right

* Use events when you should
    * Synchronous coupling is not a good substitute for event-driven architecture.
    * Old paradigms are supplemented, not supplanted.
* Embrace database appropriately
    * Change data capture lets data-in-motion and data-at-rest coexist.
* Manage your schemas
    * Schema matters: durable event logs can be used by other systems
* Use appropriate compute frameworks
    * There are Kafka tools to handle: Kafka Connect, Kafka Streams, ksqlDB
* Managed services whenever you can