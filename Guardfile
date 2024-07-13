require "active_support/inflector"
# A sample Guardfile
# More info at https://github.com/guard/guard#readme

## Uncomment and set this to only include directories you want to watch
# directories %w(app lib config test spec features) \
#  .select{|d| Dir.exist?(d) ? d : UI.warning("Directory #{d} does not exist")}

## Note: if you are using the `directories` clause above and you are not
## watching the project directory ('.'), then you will want to move
## the Guardfile to a watched dir and symlink it back, e.g.
#
#  $ mkdir config
#  $ mv Guardfile config/
#  $ ln -s config/Guardfile .
#
# and, you'll have to watch "config/Guardfile" instead of "Guardfile"

guard :minitest, all_on_start: false do
  watch(%r{^test/(.*)\/?test_(.*)\.rb$})
  watch(%r{^test/test_helper\.rb$}) { 'test' }
  watch('config/routes.rb') { interface_tests }
  watch(%r{app/views/layouts/*}) { interface_tests }

  watch(%r{^app/models/(.*)\.rb$}) do |matches|
    [
      "test/models/#{matches[1]}_test.rb",
      "test/integration/microposts_interface_test.rb",
    ]
  end

  watch(%r{^test/fixtures/(.*?)\.yml$}) do |matches|
    "test/models/#{matches[1].singularize}_test.rb"
  end

  watch(%r{^app/mailers/(.*?)\.rb$}) do |matches|
    "test/mailers/#{matches[1]}_test.rb"
  end

  watch(%r{^app/views/(.*)_mailer/.*$}) do |matches|
    "test/mailers/#{matches[1]}_mailer_test.rb"
  end

  watch(%r{^app/controllers/(.*?)_controller\.rb$}) do |matches|
    resource_tests(matches[1])
  end

  watch(%r{^app/views/([^/]*?)/.*\.html\.erb$}) do |matches|
    controller_test(matches[1]) + integration_tests(matches[1])
  end

  watch(%r{^app/helpers/(.*?)_helper\.rb$}) do |matches|
    integration_tests(matches[1])
  end

  watch('app/views/layouts/application.html.erb') do
    'test/integration/site_layout_test.rb'
  end

  watch('app/helpers/sessions_helper.rb') do
    integration_tests << 'test/helpers/sessions_helper_test.rb'
  end

  watch('app/controllers/sessions_controller.rb') do
    controller_test('sessions') + ['test/integration/users_login_test.rb']
  end

  watch('app/controllers/account_activations_controller.rb') do
    'test/integration/users_signup_test.rb'
  end

  watch(%r{app/views/users/*}) do
    resourse_tests('users') +
    ['test/integration/microposts_interface_test.rb']
  end

  watch('app/controllers/relationships_controller.rb') do
    controller_test('relationships') + ['test/integration/following_test.rb']
  end

  def integration_tests(resourse = :all)
    if resource == :all
      Dir["test/integration/*"]
    else
      Dir["test/integration/#{resource}_*.rb"]
    end
  end

  def interface_tests
    integration_tests << "test/controllers"
  end

  def controller_test(resource)
    "test/controllers/#{resource}_controller_test.rb"
  end

  def resource_tests(resource)
    integration_tests(resource) << controller_test(resource)
  end
end
