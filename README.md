# 🔥 Hot Tips 🔥
# Rails / Ruby 

### Rails: Skip Callbacks When Needed

**Instead of this:**

````ruby 
@user.last.update_attributes(
  f_name: 'Michael',
  email: 'mscott@dundermifflin.com'
)

# Some callback hell side effect
````


**You can do:**

````ruby
@user.last.update_columns(
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

### Rails / Ruby: `try` Quick way to deal with nil blowing shit up 💥 

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

*Note: There is also the `safe navigation` operator - `user.address.&zip_code` that does essentially the same thing -  however - this is only available in ruby >2.3*




# JavaScript 

WBBJS: 
### Variables `const` all the time unless I need to change the variable, then it's `let` 


### `` `backticks` `` allow multi-line strings and `"` within them. 

example: 

````js 

   const html = `
      <div class="container">
        <h2>${name}</h2>
        <p>${hello}</p>
      </div>
    `;


````

### All JS Types

**SNOBUSN**

- **S**tring
- **N**umber
- **B**oolean 
- **O**bject
- **U**ndefined
- **S**ymbol
- **N**ull

### `===` vs `==` 

We Bos: "Almost always you should use `===`"

`===` checks for value and type

Example: 

- `10 === 10 // true` 
-  `10 == 10 // true` 
- `10 == "10" // true`
- `10 === "10" // false`

### JavaScript Function Breakdown 

![funciton breakdown](https://i.imgur.com/bljcORs.png)

### Passing Functions into functions 

```js 

// Passing functions into functions 
function doctorize(name) {
  return `Dr. ${name}`;
}

doctorize('John'); // Dr. John

function yell(name) {
  return `HEY ${name.toUpperCase()}`;
}

yell(doctorize('john')); // HEY DR. JOHN

function reverse(string) {
  return string.split("").reverse().join("");
}

reverse(yell(doctorize('john'))); // NHOJ .RD YEH



```

