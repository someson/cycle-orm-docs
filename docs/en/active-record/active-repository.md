# Active Repository

Repositories provide a layer of abstraction between your domain/business logic and the data access layer.
They encapsulate the query building logic and provide a consistent interface for working with your data.

ActiveRepository combines the advantages of the [classic ORM Repository](/docs/en/basic/repository.md) and the [ActiveQuery](/docs/en/active-record/active-query.md):

- Immutable by default
- Can be associated with an entity, or not
- No restriction "an entity can have only one repository"
- Not a `QueryBuilder` entity, so it can follow a contract with a limited set of methods.
- Organically used in the DI container


The `ActiveRepository` class provides a set of methods to interact with your entities:

- Fetching data: `findOne`, `findAll`, `findByPK`
- Query building: `select`, `forUpdate`
- Protected methods for customizations: `with`, `initSelect`

## Defining a Repository

To define a repository, create a class that extends the `ActiveRepository` class and optionally implements a contract:

```php
interface UserRepositoryInterface
{
    public function getByEmail(string $email): User;

    public function whereActive(bool $active = true): static;

    public function withPosts(): static;
}
```

In the implementation, we can reuse any [Active Query](/docs/en/active-record/active-query.md) class
to replace the main Select object inside the repository.

```php
/**
 * @extends ActiveRepository<User>
 */
class UserQuery extends ActiveQuery
{
    // ...

    public function active(bool $active = true): static { ... }

    public function withPosts(): static { ... }
}
```

Now we are ready to implement the repository.
We should keep in mind that the repository is designed to be immutable.
That's why we have to use the `$this->select()` method that returns a cloned instance of the main Select object,
so we can safely modify it.

In immutable chaining methods, we should return a new instance of the repository,
and the `with(Select $select)` method helps us to do that in a convenient way.

```php
/**
 * @method UserQuery select()
 * @extends ActiveRepository<User>
 */
class UserRepository extends ActiveRepository implements UserRepositoryInterface
{
    // Redefine the constructor to hardcode the entity class
    public function __construct()
    {
        parent::__construct(User::class);
    }

    // Replace the main Select object with the custom UserQuery
    public function initSelect(ORMInterface $orm, string $role): UserQuery
    {
        return new UserQuery();
    }

    // How to build a query
    public function getByEmail(string $email): User
    {
        return $this->select()->where('email', $email)->fetchOne() ?? throw new NotFoundException();
    }

    // How to write an immutable method
    public function whereActive(bool $active = true): static
    {
        return $this->with($this->select()->active());
    }

    public function withPosts(): static
    {
        return $this->with($this->select()->withPosts());
    }
}
```

Now the repository may be bound to the DI container or used directly in the code:

```php
$repository = new UserRepository();
$user = $repository->getByEmail($email);

$activeUsers = $repository
    ->whereActive()
    ->withPosts()
    ->findAll();
```
