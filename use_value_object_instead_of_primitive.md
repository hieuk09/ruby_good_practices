## Use value object instead of primitive

Example:

```ruby
# Not prefer

def convert(amount, from_currency, to_currency)
  # ...
end

transaction.amount = 100
transaction.currency = 'usd'
puts convert(transaction.amount, transaction.currency, 'vnd')

# Prefer

class Money
  def initialize(amount, currency)
    # ...
  end

  def convert_to(to_currency)
    # ...
  end
end

transaction.amount = Money.new(100, 'usd')
puts transaction.amount.convert_to('vnd')
```

## Reason

- Business logic is better organized into specific object
- Easier to reuse
- The fields that are used together are coupled into a single object, which
reduce the chances of bug that happens because we forget updating a field.
