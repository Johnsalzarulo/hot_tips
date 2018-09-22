# 🔥 Hot Tips 🔥
# Rails / Ruby / WebDev Hot tips

### Rails: Skip Callbacks When Needed

**Instead of this:**

````ruby 
@user.last.update_columns(
  f_name: 'Michael',
  email: 'mscott@dundermifflin.com'
)

# Some callback hell side effect
````


**You can do:**

````ruby
@user.last.update_attributes(
  f_name: 'Michael',
  email: 'mscott@dundermifflin.com'
)

# No callback hell side effects!
````

**OR, just be more careful with callbacks!** 


### Rails / Ruby: Performing a method on a collection of objects
When performing a method on a collection of objects. You can just pass your method as an argument to .each 

**When you need to do:**

````ruby
notifications.each do |notification|
  notification.dismiss!
end
````

**You can do:**

````ruby
 notifications.each(&:dismiss)
````

### Rails / Ruby: Use Next 

**When you need to do:**

````ruby 
[0,1,2,3].each do |item|
  if item > 1 
    puts item
  end
end
````

**You can do:** 

````ruby 
[0,1,2,3].each do |item|
  next unless item > 1
  puts item
end
````

### Rails / Ruby: TRY // Quick way to deal with nil 

**When you need to do:**

````ruby

  # ASSUME
  # We have a user that has_one primary_address. 
  # A PrimaryAddress has many attributes including a zip code. 
  
  # When user has a primary address with zip code
  
  user.address.zip_code
  # Returns "93001" 
  
  # However when a user does not have a primary address: 
  
  user.address.zip_code
  # BLOWS THINGS UP
  # NoMethodError: undefined method `zip_code' for nil:NilClass
  
````

**You can do:**

````ruby

  # When user has a primary address with zip code
  
  user.address.try(:zip_code)
  # Returns "93001" 
  
  user.address.try(:zip_code)
  # Returns nil and doesn't blow things up. 
  
 
````





