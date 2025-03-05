# Prototype Pattern

The Prototype pattern is used to create objects based on a template of an existing object through cloning. It's useful for defining methods and properties that should be shared across all instances of a particular type, promoting efficient memory usage and consistent behavior.

### Example

```js
// Define a constructor function
function Person(name, age) {
  this.name = name;
  this.age = age;
}

// Add a method to the prototype
Person.prototype.greet = function () {
  console.log(`Hello, my name is ${this.name} and I am ${this.age} years old.`);
};

// Create instances
const person1 = new Person("Alice", 30);
const person2 = new Person("Bob", 25);
```

### Explaining the code

1. **Constructor Function:**

   - The `Person` function is a constructor that initializes new objects with `name` and `age` properties.

2. **Prototype Method:**

   - The `greet` method is added to the `Person.prototype`. This means that all instances of `Person` will share this method, rather than each instance having its own copy. This promotes memory efficiency.

3. **Instance Creation:**

   - Two instances of `Person` are created using the `new` keyword. `person1` and `person2` are objects with their own `name` and `age` properties.

### Usage

```js
person1.greet(); // Output: Hello, my name is Alice and I am 30 years old.
person2.greet(); // Output: Hello, my name is Bob and I am 25 years old.
```

- The `greet` method is called on each instance, demonstrating that each instance can access the shared method and use its own properties.

### Summary

The Prototype pattern is particularly useful in scenarios where object creation is resource-intensive or when you need to ensure uniform behavior across multiple instances.
