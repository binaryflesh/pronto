# Changelog
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](http://keepachangelog.com/en/1.0.0/)
and this project adheres to [Semantic Versioning](http://semver.org/spec/v2.0.0.html).

## [Unreleased]
[Unreleased]: https://github.com/althonos/pronto/compare/v1.1.4...HEAD

## [1.1.4] - 2020-01-21
[1.1.3]: https://github.com/althonos/pronto/compare/v1.1.3...v1.1.4
### Added
- Explicit support for Python 3.8.
- Support for Windows-style line endings
  ([#53](https://github.com/althonos/pronto/issues/53))

## [1.1.3] - 2019-11-10
[1.1.3]: https://github.com/althonos/pronto/compare/v1.1.2...v1.1.3
### Fixed
- Handling of some clauses in `FastoboParser`.
- `OboSerializer` occasionaly missing lines between term and typedef frames.
### Added
- Missing docstrings to some `Entity` properties.

## [1.1.2] - 2019-10-30
[1.1.2]: https://github.com/althonos/pronto/compare/v1.1.1...v1.1.2
### Fixed
- `RdfXMLParser` crashing on entities with `rdf:label` elements
  without literal content.

## [1.1.1] - 2019-10-29
[1.1.1]: https://github.com/althonos/pronto/compare/v1.1.0...v1.1.1
### Fixed
- `pronto.serializers` module not being embedded in Wheel distribution.

## [1.1.0] - 2019-10-24
[1.1.0]: https://github.com/althonos/pronto/compare/v1.0.0...v1.1.0
### Added
- `Entity.add_synonym` method to create a new synonym and add it to an entity.
- `@roundrepr` now adds a minimal docstring to the generated `__repr__` method.
- `Ontology` caches subclassing relationships to greatly improve performance of
  `Term.subclasses`.
### Changed
- `Entity` subclasses now store their `id` directly to improve performance.
- `Term.subclasses` and `Term.superclasses` use `collections.deque` instead of
  `queue.Queue` as a LIFO structure since thread-safety is not needed.
- `chardet` result is now used even when prediction confidence is under 100%
  to detect encoding of the handle passed to `Ontology`.
### Fixed
- `SynonymType` comparison implementation.
- `Synonym.type` getter crashing on `type` not being `None`.
- `RdfXMLParser` crashing on synonymtypedefs without scope specifiers.

## [1.0.0] - 2019-10-11
[1.0.0]: https://github.com/althonos/pronto/compare/v1.0.0-alpha.3...v1.0.0
### Fixed
- Issues with typedef serialization in `FastoboSerializer`.
- `Ontology.create_term` and `Ontology.create_relationship` not raising `ValueError`
  when given an identifier already in the knowledge graph.
- Signature of `BaseSerializer.dump` to remove `encoding` argument.
- Missing `__slots__` in `Entity` in non-typechecking runtime.
### Changed
- Bumped `fastobo` requirement to `v0.6.0`.

## [1.0.0-alpha.3] - 2019-10-10
[1.0.0-alpha.3]: https://github.com/althonos/pronto/compare/v1.0.0-alpha.2...v1.0.0-alpha.3
### Added
- Extraction of `oboInOwl:consider` annotation in `RdfXMLParser`.
- Extraction of `oboInOwl:savedBy` annotation in `RdfXMLParser`.
- Extraction of `subsetdef` and `synonymtypedef` as annotation properties in
  `RdfXMLParser`.
- Support for `doap:Version` instead of `owl:VersionIri` for specification
  of ontology data version.
- Proper comparison of `PropertyValue` classes, based on the lexicographic order
  of their serialization.
- `Ontology.dump` and `Ontology.dumps` methods to serialize an ontology in
  **obo** or **obojson** format.
### Fixed
- `Metadata` not storing optional description of ID spaces if any.
- Wrong type hints in `RelationshipData.equivalent_to_chain`.
### Changed
- Added type checking to some more property setters.
- Avoid using `networkx` in `Term.subclasses`.
- `fastobo`-derived parsers will not create a new entity if one exists in the
  graph of dependencies already.
- Exposed `pronto.warnings` and the complete warnings hierarchy.

## [1.0.0-alpha.2] - 2019-10-03
[1.0.0-alpha.2]: https://github.com/althonos/pronto/compare/v1.0.0-alpha.1...v1.0.0-alpha.2
### Added
- Support for extraction of relationships from OWL/XML files to `OwlXMLParser`.
### Fixed
- Type hints of `RelationshipData.synonyms` attribute.

## [1.0.0-alpha.1] - 2019-10-02
[1.0.0-alpha.1]: https://github.com/althonos/pronto/compare/v0.12.2...v1.0.0-alpha.1
### Changed
- Dropped support for Python earlier than `3.6`.
- Brand new data model that follow the OBO 1.4 object model.
- Partial OWL XML parser implementation using the OBO 1.4 semantics.
- New OBO parser implementation based on `fastobo`.
- Imports are properly separated from the top-level ontology.
- `Ontology.__getitem__` can also access entities from imports.
- `Term`, `Relationship`, `Xref`, `SynonymType` compare only based on their ID.
- `Subset`, `Definition` compare only based on their textual value.
### Added
- Support for OBO JSON parser based on `fastobo`.
- Provisional `mypy` type hints.
- Type checking for most properties in `__debug__` mode.
- Proper `repr` implementation that should roundtrip most of the time.
- Detection of file format and encoding based on buffer content.
### Removed
- OBO and JSON serialization support (for now).
- `Term.rchildren` and `Term.rparents` and stop making direction assumptions on relationships.
