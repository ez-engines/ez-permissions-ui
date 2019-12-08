# Ez::Permissions::UI

### Configuration

Configuration interface allows you to change default behavior
```ruby
Ez::Permissions.configure do |config|
  # Use permissions UI capabilities
  require 'ez/permissions/ui'

  # Define your base UI controller and routes
  config.ui_base_controller = 'ApplicationController'
  config.ui_base_routes = '/permissions'

  # Add custom code to Ez::Permissions::RolesController
  config.ui_roles_controller_context = proc do
    before_action :authorize_user!
    before_action do
      Ez::Permissions::API.authorize!(current_user, :manage, :permissions)
    end
  end

  # Add custom code to Ez::Permissions::PermissionsController
  config.ui_permissions_controller_context = proc do
    before_action :authorize_user!
    before_action do
      Ez::Permissions::API.authorize!(current_user, :manage, :permissions)
    end
  end

  # By default actions ordered by name  as create > read > update > delete
  config.ui_actions_ordering = %w[list create read update delete]

  # Permissions UI ships with default generated CSS classes.
  # You always can inspect them in the browser and override
  config.ui_custom_css_map = {
    'ez-permissions-roles-container' => 'you custom css classes here'
  }
end
```

### UI routes
In your `routes.rb`

```ruby
Rails.application.routes.draw do
  namespace :admin do
    ez_permissions_ui_routes
  end
end
```

## TODO
- [ ] Cached permissions. If single UI has multiple checks for one user - we can cache it!
- [ ] Not all permissions should be manageable through UI, like roles and permissions.

## Contributing
Contribution directions go here.

## License
The gem is available as open source under the terms of the [MIT License](https://opensource.org/licenses/MIT).
