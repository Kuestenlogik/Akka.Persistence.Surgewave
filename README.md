# Akka.Persistence.Surgewave

Akka.NET Persistence plugin backed by [Surgewave](https://github.com/Kuestenlogik/Surgewave) — Journal, Snapshot Store, and Persistence Query with Schema Registry support.

> **NuGet PackageId:** `Kuestenlogik.Akka.Persistence.Surgewave` &nbsp;·&nbsp; **Namespace:** `Kuestenlogik.Akka.Persistence.Surgewave`
>
> The `Akka.*` prefix on nuget.org is verified-reserved by the Akka.NET team, so this package — and the C# namespaces it ships — live under the `Kuestenlogik.*` prefix (Petabridge pattern, consistent with the rest of the Kuestenlogik / Surgewave package family).

## Installation

```bash
dotnet add package Kuestenlogik.Akka.Persistence.Surgewave
```

```csharp
using Kuestenlogik.Akka.Persistence.Surgewave;
```

> **v0.2.0 Breaking Change:** the C# namespace was renamed from `Akka.Persistence.Surgewave` to `Kuestenlogik.Akka.Persistence.Surgewave` so the on-disk source tree, the NuGet package id and the namespace are aligned. v0.1.1 consumers need to update their `using` statements.

## Features

- **AsyncWriteJournal** — Surgewave-backed event journal with index-based fast replay
- **SnapshotStore** — Compacted topic for automatic snapshot lifecycle
- **Persistence Query** — EventsByPersistenceId, EventsByTag, AllEvents (live + current)
- **Two Serialization Modes** — Opaque (Akka serializer passthrough) and Schema Registry (Protobuf/Avro/JSON)
- **Schema Registry Integration** — Events become first-class citizens in the Surgewave ecosystem
- **Exactly-Once Semantics** — Optional transactional writes for AtomicWrite guarantees
- **Multi-Tenancy** — Topic prefix support for multiple actor systems on the same cluster

## Quick Start

```csharp
builder.Services.AddAkka("my-system", (akkaBuilder, sp) =>
{
    akkaBuilder
        .WithSurgewavePersistence(surgewave =>
        {
            surgewave.BootstrapServers = "localhost:9092";
            surgewave.Journal.Topic = "akka-journal";
            surgewave.Snapshots.Topic = "akka-snapshots";
            surgewave.SchemaRegistry.Url = "http://localhost:8081";
        })
        .WithSurgewaveReadJournal();
});
```

## License

Apache-2.0
