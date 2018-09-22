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







