### Avoid external side effect when using transactions

- Transaction here means transaction of database.

- External side effect can be:

  + A modification in an external database
  + A modification in an external service

Example:

```ruby
# not prefer
ActiveRecord::Base.transaction do
  notification = Notification.create!
  Mailer.send_notification(notification.id)
  post.increase!(:notification_count)
end

# prefer
ActiveRecord::Base.transaction do
  notification = Notification.create!
  post.increase!(:notification_count)
end

Mailer.send_notification(notification.id)
```

### Reason

Normal database system cannot rollback changes in external system when a
ROLLBACK request is issued. If we do like the "not prefer" part in the example, we
can have a situation where a notification is mailed to user but the actual
notification is not created.
