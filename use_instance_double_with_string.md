## Use instance double with string instead of class

Example:

```ruby
# not prefer
user = instance_double(User, id: 1)

# prefer
user = instance_double('User', id: 1)
```

## Reason

- Using string allows tests to be passed even before concrete class is
implemented (in the above case `User`), this is extremely helpful if you codes
in TDD-top-down style: you don't have to define `User` class before working on
the consumer of that class. The test will only fail when running the whole test
suites, when you're probably finish with all the code at that time.

- You don't have to require the file which defines `User` directly in the tests.
In Rails, this means that you don't need to require `rails_helper`, but can use
`spec_helper` instead. This make the test file cleaner.
