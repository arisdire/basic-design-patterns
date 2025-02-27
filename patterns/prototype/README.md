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

1. **Constructor Function:** `Person` is a constructor function used to create new objects with `name` and `age` properties.
2. **Prototype Method:** The `greet` method is added to `Person.prototype`, so all instances of `Person` can use this method without duplicating it for each instance.
3. **Instance Creation:** `person1` and `person2` are instances of `Person`, created using the `new` keyword.
4. **Method Invocation:** The `greet` method is called on each instance, demonstrating how each instance can access shared methods.
