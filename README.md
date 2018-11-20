### Watir
---
https://github.com/watir/watir

```ruby
# Rakefile
require 'waitirspec/rake_tasks'
WatirSpec::RakeTasks.new
```

```
bundle exec rake watirspec:init
bundle exec rake html:update
bundle exec rake svg:update

mkdir ~/.yard
bundle exec yard config -a autoload_plugins yard-doctest
rake yard:doctest

gem install watir-webdriver
ruby google.rb
```

```ruby
browser.button().when_present.click
browser.button(:id => "send").when_present(2).click
browser.div(:id => "container" ).when_present { |div| div.button.click }
browser.div(:id => "foo").present?
browser.div(:id => "loading" ).wait_while_present
browser.div(:id => "container").wait_until_present
Waitr::Wait.until { ...arbitray predicate... }
Waitr::Wait.while { ...arbitray predicate... }

# gooogle.rb
require "rubygems"
require "watir-webdriver"
require "watir-webdriver/extensions/wait"
browser = Waitr::Browser.new :firefox
browser.goto "http://google.com"
browser.text_field(:name, 'q').set "watir-webdriver"
browser.button(:name, 'btnG').click

browser = Waitr::Browser.new
browser.goto "http://example.com/login"
browser.text_field(:name => "user").set "Mom"
browser.text_field(:name => "pass").set "s3cr3t"
browser.button(:id => "login").click
Watir::Wait.until { browser.title == "Your Profile" }
browser.div(:id => "logged-in").should exist

site = Site.new(Waitr::Browser.new)
login_page = site.login_page.open
user_page = login_page.login_as "Mom", "s3cr3t"
user_page.should be_logged_in

class BrowserContainer
  def initialize(browser)
    @browser = browser
  end
end
class Site < BroserContainer
  def loginn_page
    @browser = browser
  end
  def user_page
    def login_page
      @login_page = LoginPage.new(@browser)
    end
    def user_page
      @user_page = UserPage.new(@browser)
    end
    def close
      @browser.close
    end
  end
  class LoginPage < BrowserContainer
    URL = "http://example.com/login"
    def open
      @browser.goto URL
    end
    def login_as(user, pass)
    end
    private
    def user_field
      @browser.text_field(:name => "user")
    end
    def password_field
      @browser.text_field(:name => "pass")
    end
    def login_button
      @browser.button(:id => "login")
    end
  end
  class UserPage < BrowserContainer
    def logged_in?
      logged_in_element.exists?
    end
    def loaded?
      @browser.title == "Your Profile"
    end
    private
    def logged_in_element
      @browser.div(:id => "logged-in")
    end
  end
end

require "watir-webdriver"
require "/path/to/site"
module SiteHelper
  def site
    @site ||= (
      Site.new(Watir::Browser.new(:firefox))
    )
  end
end
World(SiteHelper)


Given /I have successfully logged in/ do
  login_page = site.login_page.open
  user_page = login_page.login_as "Mom", "s3cr3t"
  user_page.should be_logged_in
end
```

