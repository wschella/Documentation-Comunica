# Query Operations

Query operations are a key element in comunica for query evaluation.
These operations are based on SPARQL Algebra, and use the TypeScript types provided by [SPARQLAlgebra.js](https://github.com/joachimvh/SPARQLAlgebra.js).

[`@comunica/bus-query-operation`](https://github.com/comunica/comunica/tree/master/packages/bus-query-operation) is the bus on which actors can subscribe to perform certain query operations.
[`@comunica/actor-query-operation-quadpattern`](https://github.com/comunica/comunica/tree/master/packages/actor-query-operation-quadpattern) is for instance responsible for evaluating quad patterns.

Operations take a certain operation as input, together with an optional _context_.
The output is a [`BindingsStream`](https://github.com/comunica/comunica/blob/master/packages/bus-query-operation/lib/Bindings.ts#L13), a set of variable names that occur in the bindings stream and optional _metadata_.
The input context and output metadata are optional hashes that can contain additional information that can help certain actors.
We describe all currently available context and metadata entries hereafter.

## Context Entries

| Name         | Related Actors | Description |
| ------------ | -------------- | ----------- |
| `sources` | `@comunica/actor-rdf-resolve-quad-pattern-qpf` | A list of source objects and their type, e.g. `{ type: 'hypermedia', value: 'http://fragments.dbpedia.org/2016-04/en'}` |

Currently supported types are `sparql`, `hypermedia` (for TPF and similar variants), `hdt` (for a local HDT file) and `file` (for a local turtle file).

## Metadata Entries

| Name         | Related Actors | Description |
| ------------ | -------------- | ----------- |
| `searchForms` | `@comunica/actor-rdf-resolve-quad-pattern-qpf`, `@comunica/actor-rdf-metadata-extract-hydra-controls` | The available Hydra search forms on a certain page. |
| `totalItems` | `@comunica/actor-rdf-resolve-quad-pattern-qpf`, `@comunica/actor-rdf-metadata-extract-hydra-count` | An estimate of the total number of items in a collection. |