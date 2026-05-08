# Akka.Persistence.Surgewave — Roadmap

## v0.1 — Journal + Snapshot (Hyperion) [done]

- [x] SurgewaveJournal (AsyncWriteJournal) with index-based fast replay
- [x] SurgewaveSnapshotStore using compacted topics
- [x] OpaqueEventSerializer (Akka Hyperion passthrough)
- [x] HOCON configuration and Akka.Hosting DI extensions
- [x] Akka.NET TCK test specs (JournalSpec, SnapshotStoreSpec)
- [x] Lazy async initialization (EnsureInitializedAsync)
- [x] Capture Context.System in constructor (async-safe)

## v0.2 — Schema Registry Integration (JSON) [done]

- [x] SchemaRegistryEventSerializer with Confluent wire format
- [x] Auto-registration of JSON schemas via ISchemaRegistryOperations
- [x] Type resolution from akka-manifest header
- [x] Schema ID caching per type
- [x] SchemaRegistryOperations injected via SurgewaveNativeClient.Schema (lazy)

## v0.3 — Protobuf Serialization [done]

- [x] Proto mode: IMessage.ToByteArray() for serialize, Parser.ParseFrom for deserialize
- [x] Automatic schema type detection (PROTOBUF vs JSON based on IMessage)
- [x] Content-type headers: application/x-hyperion, application/json, application/x-protobuf
- [x] SerializationMode enum: Hyperion, Json, Proto (renamed from Opaque/SchemaRegistry)

## v0.4 — Persistence Query [done]

- [x] SurgewaveReadJournal (IReadJournalProvider)
- [x] EventsByPersistenceId (live + current)
- [x] EventsByTag with header-based filtering (Option A)
- [x] AllEvents (live + current)

## v0.5 — Index + Topic Management [done]

- [x] JournalIndexManager with compacted index topic and LRU cache
- [x] TopicManager: auto-create journal/snapshot/index topics on first use
- [x] Correct cleanup.policy per topic (delete, compact)
- [x] Surgewave Native Client admin API for topic creation

## v0.6 — DI + Hosting [done]

- [x] WithSurgewavePersistence() fluent configuration
- [x] WithSurgewaveReadJournal() fluent configuration
- [x] HOCON generation from typed setup objects
- [x] Multi-tenant topic prefix support
- [x] HOCON serialization-mode values: "hyperion", "json", "proto"

## v0.7 — Tests [done]

- [x] EventEnvelopeCodecTests (roundtrip, big-endian, constants)
- [x] SurgewaveJournalSettingsTests (HOCON parsing, defaults, topic prefix, mode names)
- [x] IndexEntryTests (defaults, with-expression)
- [x] SurgewaveReadJournalSpec (identifier check)
- [x] E2E integration test with embedded in-memory Surgewave broker
- [x] Actor persist → Surgewave topic → Consumer roundtrip verified

## v1.0 — Production Ready

- [ ] Exactly-Once Semantics via Surgewave TransactionBuilder
  - Requires SurgewaveNativeClient.Transactions instead of IProducer
  - TransactionBuilder.InitAsync() -> Produce -> CommitAsync()/AbortAsync()
- [ ] E2E test for Json/Proto mode (requires Schema Registry in embedded broker)
- [ ] Avro serialization mode
- [ ] Replay performance benchmarks (index vs. full scan)
- [ ] Circuit breaker integration (Akka built-in)
- [ ] Migration tooling from Akka.Persistence.PostgreSql
- [ ] NuGet package publish

## Future

- [ ] EventsByTag Option C: Surgewave.Streams tag materialization
- [ ] Tag secondary topics for high-volume EventsByTag
- [ ] PlainPartitionedSource rebalance handling in ReadJournal
- [ ] Content-type auto-deserialization via Surgewave Client (when available)
- [ ] Testcontainers.Surgewave for CI/CD integration tests
