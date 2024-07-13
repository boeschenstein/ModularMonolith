# Modular Monolith

Training from ardalis: <https://dometrain.com/bundle/from-zero-to-hero-modular-monoliths-in-dotnet/>

<https://www.milanjovanovic.tech/blog/modular-monolith-communication-patterns>

## My thoughts

- watch ardalis to type for hours
- example uses EF + SQL Server
- repo pattern, but no generic repo
- no regular or minimal API, instead he uses <https://fast-endpoints.com/>
  - needs special packages for security, swagger
- uses MediatR
  - configured to load from different assemblies
- uses Microsoft Identity

## Module Communication options

1. ask for it over HTTP --> slow, high coupling
2. just query the book table directly --> high coupling
3. call /books/{id} over http --> slow, high coupling
4. call BookService directly --> high coupling
5. make a loosely-coupled call via MediatR --> ok
6. use materialized view --> ok (part 2 of this training)

## Learnings

- if you have 1 database: separate data using db-schema
- modules (assemblies for books and users) communicate by MediatR
  - book module
  - user module, contains cart
- needs an additional module (assembly)
  - move request/response class to this contracts module
  - move MediatR queries and handlers to an \integration folder
  - avoid global contracts module - have one for each module
