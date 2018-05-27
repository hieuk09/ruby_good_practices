## [Flag argument](https://martinfowler.com/bliki/FlagArgument.html)

> A flag argument is a kind of function argument that tells the function to carry out a different operation depending on its value.

> My general reaction to flag arguments is to avoid them.

Example:

```ruby
# Not prefer

def save(is_create = true)
  if is_create
    # do create stuff
  else
    # do update stuff
  end
end

# Prefer

def create
  # do create stuff
end

def update
  # do update stuff
end
```

Example 2: when writing cucumber steps:

```ruby
# Not prefer

When('user goes to {string} page') do |page_name|
  case page_name
  when 'user'
    # go to user page
  when 'admin'
    # go to admin page
  #...
  end
end

# Prefer

When('user goes to user page') do
  # go to user page
end

When('user goes to admin page') do
  # go to admin page
end
```

## Reason

- The code is much simpler
- Decouple the switch-case logic with actual implementation, most of the time,
  you don't even need the switch because you can decide at implementation time
  because of the context (like example 2)
