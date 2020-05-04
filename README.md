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


### HTML / Rails Form Patterns 
How did I not know that raw HTML can validate a pattern on input? It's supported by [all major browsers](https://caniuse.com/#feat=input-pattern).

**ERB** (You could do this in vanila HTML as well) 

```erb 
 <%= f.text_field :email, class: "form-control", placeholder: "hello@getmainstreet.com", pattern: "^[a-zA-Z0-9_.+-]+@(?:(?:[a-zA-Z0-9-]+\.)?[a-zA-Z]+\.)?(getmainstreet)\.com$", title: "The email must be of domain getmainstreet.com" %>

```
**Result**

![Default pattern matching HTML](https://p50.f0.n0.cdn.getcloudapp.com/items/NQuD78QG/Screen%20Shot%202020-05-04%20at%202.28.12%20PM.png?v=6175987decb28e4bfe3db9b02a4a75c6)


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
function doctorize(name) {
  return `Dr. ${name}`;
}

doctorize("John"); // Dr. John

function yell(name) {
  return `HEY ${name.toUpperCase()}`;
}

yell(doctorize("john")); // HEY DR. JOHN

function reverse(string) {
  return string
    .split("")
    .reverse()
    .join("");
}

reverse(yell(doctorize("john"))); // yell(doctorize('john'));



```


### Default Variables in JS 

```js 
function greet(name = "Silly Goose", greeting = "Hey") {
  return `${greeting.toUpperCase()} ${name.toUpperCase()}`;
}

greet(); // HEY SILLY GOOSE 

greet('John', undefined) // HEY JOHN 

greet(undefined, 'Hello') // HELLO SILLY GOOSE

greet('John', 'Hello') // HELLO JOHN

```

### Methods in JavaScript Objects 
This is so fucking powerful, it's like a little lightweight ruby model!

```js
const john = {
  name: "John Jacob",
  sayHi: function() {
    return `Hey ${this.name}`;
  },
  yellHi: function() {
    return `HEY ${this.name.toUpperCase()}`;
  },
  // Arrow function
  wisperHi: function() {
    return `hi ${this.name.toLowerCase()}`;
  }
};

john.name; // 'John Jacob' 

john.sayHi(); // "Hey John Jacob"

john.yellHi(); // "HEY JOHN JACOB"

john.wisperHi(); // "hi john jacob"
``` 


### Debugging Tips 

### Console Methods
 
Given: 

```js

const people = [
  { name: 'Wes', cool: true, country: 'Canada' },
  { name: 'Scott', cool: true, country: 'Merica' },
  { name: 'Snickers', cool: false, country: 'Dog Country' },
]; 

```

`console.table(people)`returns: 

![consolelogtable](https://i.imgur.com/TAsu432.png)

### Console Group 

```js 
function doALotOfStuff() {
  console.group('Doing some stuff');
  console.log('Hey Im one');
  console.warn('watch out!');
  console.error('hey');
  console.groupEnd('Doing some stuff');
}

```

### $0 in Console 

When you select an element in chrome dev tools you can acces that element via the Javascript console with `$0` [Link to more detail](https://developers.google.com/web/tools/chrome-devtools/console/utilities?utm_campaign=2016q3&utm_medium=redirect&utm_source=dcc#dom)

### `console.dir` 

[More info on this one](https://developer.mozilla.org/en-US/docs/Web/API/Console/dir)

Essentially, it's a console.log on supper powers. It shows you every available method and attibute on the element passed into it. 

Example: 

```js 

const elementOnPage = document.getElementById("some-id");

console.dir(elementOnPage);

/// Returns a giantinteractive list of the properties of the given object. 

```

### Destructing 
[More on this topic](https://wesbos.com/destructuring-objects)

```js
// Set values from an object 
const width = canvas.width;
const height = canvas.height;
console.log(width, height);

// Or you can destructure them,
// autimatically sets and infers valid attributes from the object
const {width, height} = canvas;
console.log(width, height);

```

Another example of pulling items out: 

```js 

// write a draw function that finds and sets the values passed into it. 

function draw({ key }) {
  console.log(key);
}
// write a handler for the keys

function hanldeKey(e) {
  if (e.key.includes("Arrow")) {
    e.preventDefault();
    draw({ key: e.key });
  }
}

```


### Ternary in JS


// Ternary in JavaScript 
let word = "items" 
let count = 1

// If Statement
if (count > 1) {
  word = "items" 
} else {
  word = "item"
};

// Same If Statement as Ternary
word = count > 1 ? "items" : "item";

let sentence = `You have ${count} ${word} in your cart` // "You have 1 item in your cart"

