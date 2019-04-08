# Cycle ORM - Documentation
[![Latest Stable Version](https://poser.pugx.org/cycle/orm/version)](https://packagist.org/packages/cycle/orm)
[![Build Status](https://travis-ci.org/cycle/orm.svg?branch=master)](https://travis-ci.org/cycle/orm)
[![Scrutinizer Code Quality](https://scrutinizer-ci.com/g/cycle/orm/badges/quality-score.png?b=master)](https://scrutinizer-ci.com/g/cycle/orm/?branch=master)
[![Codecov](https://codecov.io/gh/cycle/orm/graph/badge.svg)](https://codecov.io/gh/cycle/orm)

Cycle is PHP DataMapper and ORM engine designed to work in long-running PHP applications (like [RoadRunner](https://github.com/spiral/roadrunner)).

Table of Content
----------------
* About Cycle
  * ~ [How to keep being sane while writing 60+ pages of documentation](https://github.com/cycle/docs)
  * ~ [About Cycle ORM](intro/about.md)
  * ~ [Quick Start](basic/quick-start.md)
  * ~ [Installation](into/installation.md)
  * ~ [Configuration](info/configuration.md)
  * ~ [Contributing](into/contributing.md)
  * [LICENSE](license.md)
* Basics
  * ~ [Connect to Database](basic/connetion.md)
  * ~ [Create, Update, Delete](basic/crud.md)
  * ~ [Select](basic/select.md)
  * ~ [Simple Relation](basic/relation.md)
* Annotated Entities
  * ~ [Prerequisites](annotated/prerequisites.md)
  * ~ [Entities](annotated/entity.md)
  * ~ [Relations](annotated/relations.md)
* Relations
  * ~ [Has One](relation/has-one.md)
  * ~ [Has Many](relation/has-many.md)
  * ~ [Belongs To](relation/belongs-to.md)
  * ~ [Refers To](relation/refers-to.md)
  * ~ [Many Thought Many](relation/many-though-many.md)
* Repositories
  * ~ [Select Entity](repository/select.md)
  * ~ [Relations](repository/relations.md)
  * ~ [Custom Repository](repository/custom.md)
* Query Builder
  * ~ [Basics](query-builder/basic.md)
  * ~ [Complex Conditions](query-builder/complex.md)
  * ~ [Expressions](query-builder/expressions.md)
  * ~ [Relations](query-builder/relations.md)
* Architecture
  * ~ [Overview](architecture/overview.md)
  * ~ [Schema](architecture/schema.md)
  * ~ [Entity](architecture/entity.md)
  * ~ [Collection](architecture/collection.md)
  * ~ [Pivot Collection](architecture/pivot-collection.md)
  * ~ [Heap, Node, State](architecture/heap.md)
  * ~ [Entity Iterator](architecture/iterator.md)
  * ~ [Mappers](architecture/mapper.md)
  * ~ [Commands](architecture/command.md)
  * ~ [Transactions (Unit of Work)](architecture/transaction.md)
  * ~ [Sources and Databases](architecture/source.md)
  * ~ [References, Promises and Proxies](architecture/promise.md)
  * ~ [Query Builder](architecture/query-builder.md)
  * ~ [Constrains](architecture/constrain.md)
  * ~ [Node Parser](architecture/node-parser.md)
  * ~ [Limitations](architecture/limitations.md)
* Advanced Usage
  * ~ [Usage in Long Running Applications](advanced/daemonizing.md)
  * ~ [Syncronizing Database Schema](advanced/sync-schema.md)
  * ~ [Working with Multiple Databases](advanced/multiple-databases.md)
  * ~ [Single Table Inheritance](advanced/single-table-inheritance.md)
  * ~ [Custom Mappers](advanced/custom-mapper.md)
  * ~ [Custom Commands](advanced/custom-command.md)
  * ~ [Dynamic Schema (StdClass)](advanced-/dynamic-schema.md)
  * ~ [Select Constrains](advanced-/constrain.md)
  * ~ [Caching](advanced-/caching.md)
  * ~ [References and Proxies](advanced-/references.md)
  * ~ [Testing](advanced-/testing.md)
  * ~ [Reconnects and Database Exceptions](advanced/exception.md)
  * ~ [Self-References and Cyclic Relations](advanced/cyclic.md)
  * ~ [Static Tables](advanced/static.md)
  * ~ [Custom Relations](advanced/custom-reation.md)
  * ~ [External Data Sources](advanced/external.md)
  * ~ [Configuring Schema Builder](advanced/schema-builder.md)
* Components
  * ~ [Data Mapper Core](component/core.md)
  * ~ [Schema Builder](component/schema-builder.md)
  * ~ [Annotations Parser](component/annotated.md)
  * ~ [Migrations](component/migrations.md)
  * ~ [Proxy Factory](component/proxy-factory.md)
* Integrations
  * ~ [Spiral Framework](integration/spiral.md)
