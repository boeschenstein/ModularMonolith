# Modular Monolith

<https://www.milanjovanovic.tech/blog/modular-monolith-communication-patterns>

2 Trainings from ardalis:

- Part 1: Getting Stared: <https://dometrain.com/bundle/from-zero-to-hero-modular-monoliths-in-dotnet/>
- Part 2: Deep Dive: <https://courses.dometrain.com/courses/take/deep-dive-modular-monoliths-in-net/>

## Part 1: Getting Started

### My thougts about Getting Started

- watch ardalis to type for hours
- example uses EF + SQL Server
- repo pattern, but no generic repo
- no regular or minimal API, instead he uses <https://fast-endpoints.com/>
  - needs special packages for security, swagger
- uses MediatR
  - configured to load from different assemblies
- uses Microsoft Identity (I'd prefer OAuth/OIDC approach)
- if you know how to create an ASP.NET app (EF, Repository, MediatR), don't buy this course: go directly to the 'Deep dive'

### Module Communication options

1. ask for it over HTTP --> slow, high coupling
2. just query the book table directly --> high coupling
3. call /books/{id} over http --> slow, high coupling
4. call BookService directly --> high coupling
5. make a loosely-coupled call via MediatR --> ok
6. use materialized view --> ok (part 2 of this training)

### Learnings

- if you have 1 database: separate data using db-schema
- modules (books, users) communicate by MediatR
  - book module (3 assemblies: book, book.Tests, Book.Contracts)
  - user module (contains cart)
- needs an additional module (assembly Book.Contracts)
  - no direct dependency between book and user (loosly coupled)
  - move MediatR request/response class to this contracts module
  - move MediatR queries and handlers to an \Integration folder (or "\ExternalInterface" or "\PublicInterface")
  - avoid global contracts module - have one for each module

## Part 2: Deep dive

### My thoughts about Deep Dive

### Module communication patterns

- Direct Calls : ok
  - Project reference - compile time
  - Reflection - run time
- Mediated Call (MediatR) : ok
- Shared State (DB, File, ...) : Non Blocking
- Message Bus Messages (Command, Event) : Non Blocking
- Message Bus Messages (Queries: 2 queues) : Blocking
- Store and Forward (Outbox) : Non Blocking
- Cache and Subscribe (Materialized View pattern) : Non Blocking
