## Do not abuse `present` and `blank`

When a value can be `nil` or an object, but cannot be string/array/hash, we can
use `nil?` or that value directly to check presence:

```ruby
record = Record.find_by(id: id)

# Not prefer
if record.present?
  update_record(record)
end

if record.blank?
  create_record
end

# Prefer

if record
  update_record(record)
end

if record.nil?
  create_record
end
```

When a value can be array/hash, but cannot be `nil`, it's better to use `empty?`
and `any?` instead of `blank?` and `present?`

```ruby
array = []

# Not prefer
if array.blank?
  # do something
end

if array.present?
  # do something
end

# Prefer
if array.empty?
  # do something
end

if array.any?
  # do something
end
```

## Reason

There are two reasons for this:

- Performance: `blank?` and `present?` have worse performance compared to other
similar checks.
- Maintainability: `blank?` and `present?` are too generic, which hide the
developers assumption about type of an variable. Using other checks let the
reader know what to expect from the value.
