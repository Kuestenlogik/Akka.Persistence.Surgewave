# Akka.Persistence.Surgewave — ARCHIVED

> **This repository is archived.** Active development has moved to
> [**Kuestenlogik/Akka.Surgewave**](https://github.com/Kuestenlogik/Akka.Surgewave),
> a consolidated Mono-Repo that ships **two** NuGet packages from a single tag:
> `Kuestenlogik.Surgewave.AkkaStreams` and `Kuestenlogik.Surgewave.AkkaPersistence`.

## History

- This repo published [`Kuestenlogik.Akka.Persistence.Surgewave`](https://www.nuget.org/packages/Kuestenlogik.Akka.Persistence.Surgewave) v0.1.0 and v0.1.1.
- v0.2.0+ ships only from the [Akka.Surgewave](https://github.com/Kuestenlogik/Akka.Surgewave) repo under the new id [`Kuestenlogik.Surgewave.AkkaPersistence`](https://www.nuget.org/packages/Kuestenlogik.Surgewave.AkkaPersistence).
- The v0.1.x packages remain on nuget.org for existing consumers; they receive no further updates.

## Migration

```bash
# remove old
dotnet remove package Kuestenlogik.Akka.Persistence.Surgewave
# add new
dotnet add package Kuestenlogik.Surgewave.AkkaPersistence
```

```csharp
// before
using Akka.Persistence.Surgewave;

// after
using Kuestenlogik.Surgewave.AkkaPersistence;
```

HOCON / Akka.Hosting setup is otherwise compatible — `WithSurgewavePersistence` / `WithSurgewaveReadJournal` exist in the new namespace.

## License

Apache-2.0
