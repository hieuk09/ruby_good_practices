## Create just enough data for testing

Example:

```ruby
class User < ActiveRecord::Base
  scope :active, -> { where(active: true }
end

# Prefer
let!(:inactive_user) { create(:user, active: false) }
let!(:active_user) { create(:user, active: true) }

# Maybe ok
let!(:inactive_users) { create_list(:user, 2, active: false) }
let!(:active_users) { create_list(:user, 2, active: true) }

# Not prefer
let!(:inactive_users) { create_list(:user, 3, active: false) }
let!(:active_users) { create_list(:user, 3, active: true) }
```

## Reason

Creating extra records cost time, CPU and memory. If they doesn't add any value
for the test, we should remove them.
