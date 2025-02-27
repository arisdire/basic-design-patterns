# Prototype Pattern

The Prototype pattern is used to create objects based on a template of an existing object through cloning. It's useful for defining methods and properties that should be shared across all instances of a particular type, promoting efficient memory usage and consistent behavior.

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

// Call the method
person1.greet(); // Output: Hello, my name is Alice and I am 30 years old.
person2.greet(); // Output: Hello, my name is Bob and I am 25 years old.
```

### Summary

The Prototype pattern is particularly useful in scenarios where object creation is resource-intensive or when you need to ensure uniform behavior across multiple instances.
