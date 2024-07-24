# Active Query

The `ActiveQuery` class extends Cycle ORM `Select` class
and is specifically designed to integrate with entities managed by `ActiveRecord`.
It simplifies the process of building queries and can be easily maintained and reused throughout the application.

## Standard Usage

Entities that extend the `ActiveRecord` class automatically benefit from the `ActiveQuery` capabilities through the `query()` method:

```php ActiveRecord.php
public static function query(): ActiveQuery
{
    return new ActiveQuery(static::class);
}
```

This method provides a straightforward way to begin a query operation tailored to the entity's context.

## Defining Custom Query Classes

To encapsulate specific query logic, developers can create custom query classes that extend the `ActiveQuery` class.

For example, the `CommonQuery` class might define methods to handle common requirements
such as filtering by active status or sorting by creation time:

```php CommonQuery.php
/**
 * @template T
 * @extends ActiveQuery<User>
 */
class CommonQuery extends ActiveQuery
{
    public function active(bool $state = true): static
    {
        return $this->where(['active' => $state]);
    }

    public function sortByCreateTime(bool $newestFirst = true): static
    {
        return $this->orderBy(['created_at' => $newestFirst ? 'DESC' : 'ASC']);
    }
}
```

By overriding the `query()` method in a derived entity class to return an instance of a custom query class,
developers can significantly simplify the data access layer.
This approach not only enhances code readability but also improves the organization of business logic:

```php User.php
#[Entity(table: 'user')]
class User extends ActiveRecord
{
    // ...

    /**
     * @return CommonQuery<static>
     */
    public static function query(): CommonQuery
    {
        return new CommonQuery(static::class);
    }
}
```

Now we can fetch all user records, which are not active and are ordered by `createdAt` field in descending order:

```php
$users = User::query()
    ->active(false)
    ->sortByCreateTime(false)
    ->fetchAll();
```

Now let's personalize the Active Query class to User entity:

```php UserQuery.php
/**
 * @extends CommonQuery<User>
 */
class UserQuery extends CommonQuery
{
    public function __construct()
    {
        parent::__construct(User::class);
    }

    public function emailVerified(bool $state = true): static
    {
        return $this->where(['email_verified' => $state]);
    }

    public function subscribtionLevel(Subsctiption $level): static
    {
        return $this->where('subscriptionLevel', '>=' , $level->alue);
    }
}
```

And update the `User` entity to use the `UserQuery` class:

```php User.php
#[Entity(table: 'user')]
class User extends ActiveRecord
{
    // ...

    public static function query(): UserQuery
    {
        return new UserQuery();
    }
}
```

Now we can use functions from `CommonQuery` and `UserQuery` classes:

```php
$users = User::query()
    ->active(false)
    ->emailVerified(true)
    ->subscribtionLevel(Subsctiption::Any)
    ->fetchAll();

$mailer->sendReminder($users);
```
