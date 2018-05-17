### Prefer to use customized class rather than system provided exeption

Example:

```ruby
# Not prefer
raise ArgumentError.new('user is missing')

# Prefer
class UserMissingError < BaseError
  def message
    'user is missing'
  end
end

raise UserMissingError
```

### Reason

- It's easier to catch all customized error in the top level for logging
purpose. For example, in Rails, we can:

```
# in application_controller.rb
rescue_from BaseError, with: render_expected_error
rescue_from StandardError, with: render_unexpected_error
```
