# Introduction

## What is Cycle Active Record?

This library extends Cycle ORM by integrating the [Active Record pattern](https://en.wikipedia.org/wiki/Active_record_pattern), providing developers with an intuitive, object-centric way to interact with databases.

Unlike Cycle ORM's default Data Mapper pattern, which separates the in-memory object representations from database operations, Active Record in general combines database operations and data projection in a single entity.

This allows for more straightforward and rapid development cycles, particularly for simpler CRUD operations, by enabling direct data manipulation through the object's properties and methods.

> Note
> Using the Active Record pattern does not require placing business logic inside entities.
> Use Active Record for prototyping, speeding up development, and simplifying code.
> And yes, the flexibility of Cycle ORM allows you to elegantly apply both patterns simultaneously.


## Key Features

0. **Full compatibility**: All Cycle ORM features are supported.
1. **High speed development**: Access to CRUD operations through Entity class methods and properties.
2. **New features**: Active Query, Active Repository, and more.
3. **Easy to use**: Easy to install, learn, and use.


## Contributing

The Active Record component is in active development. Any feedback and ideas are welcome.
Read our [contributing guidelines](https://github.com/cycle/active-record/blob/master/.github/CONTRIBUTING.md) to get started.
