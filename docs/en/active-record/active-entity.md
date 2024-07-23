# Active Entities

## Defining Entities

To work with the Cycle Active Record, you need to define entities that extend the `ActiveRecord` class.
There are two common approaches to defining entities: the `strict` approach and the `fluent` approach.

These approaches will be used as main examples across documentation to demonstrate various aspects of the library.

> [Cycle ORM Annotated Entities](/docs/en/annotated/entity.md)

:::: tabs

::: tab Strict

**Strict Approach:**

In the strict approach, you define your entity with private properties and provide public getter and setter methods to access and modify the properties.

This approach encapsulates the entity's internal state and provides better control over how the properties are accessed and modified.

```php
<?php

declare(strict_types=1);

namespace App\Entities;

use Cycle\ActiveRecord\ActiveRecord;
use Cycle\Annotated\Annotation\Column;
use Cycle\Annotated\Annotation\Entity;

#[Entity(table: 'users')]
class User extends ActiveRecord
{
    #[Column(type: 'bigInteger', primary: true, typecast: 'int')]
    private int $id;

    #[Column(type: 'string')]
    private string $name;

    #[Column(type: 'string', unique: true)]
    private string $email;

    public function __construct(string $name, string $email)
    {
        $this->name = $name;
        $this->email = $email;
    }

    public function id(): int
    {
        return $this->id;
    }

    public function name(): string
    {
        return $this->name;
    }

    public function changeName(string $name): void
    {
        $this->name = $name;
    }

    public function email(): string
    {
        return $this->email;
    }

    public function changeEmail(string $email): void
    {
        $this->email = $email;
    }
}
```

:::

::: tab Fluent

**Fluent Approach:**

In the fluent approach, you define your entity with public properties, allowing direct access to the properties without the need for explicit getter and setter methods.

This approach leads to more concise and readable code, especially when dealing with simple entities.

```php
<?php

declare(strict_types=1);

namespace App\Entities;

use Cycle\ActiveRecord\ActiveRecord;
use Cycle\Annotated\Annotation\Column;
use Cycle\Annotated\Annotation\Entity;

#[Entity(table: 'users')]
class User extends ActiveRecord
{
    #[Column(type: 'bigInteger', primary: true, typecast: 'int')]
    public int $id;

    #[Column(type: 'string')]
    public string $name;

    #[Column(type: 'string', unique: true)]
    public string $email;

    public function __construct(string $name, string $email)
    {
        $this->name = $name;
        $this->email = $email;
    }
}
```

:::

::::


## Select Entities

Once you have created [your first entities](defining-entities.md) and [configured](../general/installation.md) one of the adapter packages, you can begin retrieving entities from the database.

Entities that extends `ActiveRecord` class includes powerful Cycle-ORM Query Builder allowing you to fluently query the database table associated with the Entity.

Here is example with `findAll()` method, which will retrieve all of the records from the entity associated database table:

:::: tabs

::: tab Strict

Example with private properties and public getter methods. The `findAll()` method returns all the records from the `users` table, and we can access the `name` property using the `name()` method.

```php
<?php

use App\Entities\User;

$users = User::findAll();

foreach ($users as $user) {
    echo $user->name();
}
```

:::

::: tab Fluent

If you are using the fluent approach with public properties, you can directly access the properties:

```php
<?php

use App\Entities\User;

$users = User::findAll();

foreach ($users as $user) {
    echo $user->name;
}
```

:::

::::

### Building Queries

The ActiveRecord `findAll()` method will return all of the results in the entity table. However, since each ActiveRecord Entity includes a [query builder](https://cycle-orm.dev/docs/query-builder-basic/current/en), you may add additional constraints using `query()` method and then invoke the `fetchAll()` method to retrieve the results:

```php
<?php

use App\Entities\User;

$users = User::query()
    ->where('active', 1)
    ->orderBy('name')
    ->fetchAll();
```

In this example, we use the `query()` method to start building a query.

> Info
> Since ActiveRecord Entities includes access to query builder, you should review all of the methods provided by Cycle [query builder](https://cycle-orm.dev/docs/query-builder-basic/current/en). You may use any of these methods when writing your queries.

> Info
> For advanced usage of the query builder, this package provides a way to group your queries into separate Query classes by creating classes that extend the [`ActiveQuery`](../active-queries/query-classes.md) class.

### Collections

The Cycle Active Record team is constantly working on improving the library. Keep an eye on the [official repository](https://github.com/cycle/active-record) for updates and new features, such as the potential introduction of Collection support for query results.

There is currently a Proof of Concept (PoC) Pull Request for introducing Collection support for query results:

* [PR #20: Implement basic collections](https://github.com/cycle/active-record/pull/20)

If you're interested in using Collections with Cycle Active Record, you can:

1. Follow the progress of this PR
2. Contribute to the discussion by providing feedback or use cases
3. Help with the implementation if you have experience with Collections in ORMs

Contributions from the community are welcome and can significantly impact the direction and features of the library. If Collections are a feature you're particularly interested in, consider getting involved in the development process.

Remember to check the contribution guidelines before submitting any code or opening issues.
