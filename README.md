# 🔥 Hot Tips 🔥
# Rails / Ruby / WebDev Hot tips

### 🛤Rails: Skip Callbacks When Needed

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





