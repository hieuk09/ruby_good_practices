## Avoid putting full object into queue

Example:

```ruby
# Not prefer

class SomeJob < ApplicationJob
  queue_as :some_queue

  def perform(record)
    # do something with record
  end
end

SomeJob.perform_later(record)

# Prefer

class SomeJob < ApplicationJob
  queue_as :some_queue

  def perform(record_id)
    record = Record.find(record_id)
    # do something with record
  end
end

SomeJob.perform_later(record.id)
```

## Reason

Background Job library has to marshalling the object into storable type (string
or json) so that it can be saved to database (redis or mysql). When running job,
the object is parsed back to normal object and processed. This approach has two
disadvantages:

- More overhead: it has to marshall and parse data (this may be faster than
database query, though)
- Data storing as object in queue may be inconsistent with data in database. You
usually have to reload the object to make sure it's latest record.
