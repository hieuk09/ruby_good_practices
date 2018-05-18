### When writing rspec, prefer to use `instance_double` over `double`

Example:

```ruby
# not prefer
user_decorator = double('UserDecorator', email: 'email@email.com')

# prefer
user_decorator = instance_double('UserDecorator', email: 'email@email.com')
```

### Reason

`instance_double` is verified double, can verify if a method exists in an object
or not (except a few cases like metaprogramming with `method_missing`). If a
method is removed, the test of the consumer of the object fails, and we can fix
it sooner.
