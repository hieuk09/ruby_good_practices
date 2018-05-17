### When writing rspec, prefer expect over allow

```ruby
# Not prefer
allow(receiver).to receive(:activate)

# Prefer
expect(receiver).to receive(:activate)
```

### Reason

- `expect` will raise error when method is removed, which is helpful for code
removing (in case it's intentional) or bug catching (in case it's unintentional).

- `expect` will also raise error when method is called multiple times, which is
also good to know.
