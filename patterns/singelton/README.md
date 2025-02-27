# Singleton Pattern

The Singleton pattern ensures that a class has only one instance and provides a global point of access to it. This is useful when exactly one object is needed to coordinate actions across the system.

```js
class Singleton {
  // Constructor function for the Singleton class
  constructor() {
    // Check if an instance already exists
    if (!Singleton.instance) {
      // If no instance exists, assign the current instance to Singleton.instance
      Singleton.instance = this;
    }
    // Return the single instance
    return Singleton.instance;
  }

  // Example method for the Singleton class
  someMethod() {
    console.log("Singleton method called");
  }
}
```

### Explaining the code

**Class Declaration:** The `Singleton` class is declared.

**Constructor:** The constructor checks if an instance of the class already exists.

- `if (!Singleton.instance)`: This condition checks if `Singleton.instance` is `undefined` or `null`.
- `Singleton.instance = this`: If no instance exists, the current instance (`this`) is assigned to `Singleton.instance`.
- `return Singleton.instance`: The constructor returns the single instance of the class.

**Method:** The `someMethod` is a simple method that logs a message to the console.

```js
// Create the first instance of the Singleton class
const instance1 = new Singleton();
// Attempt to create a second instance of the Singleton class
const instance2 = new Singleton();

// Check if both instances are the same
console.log(instance1 === instance2); // true

// Call the method on the first instance
instance1.someMethod(); // Singleton method called
```

**Instance Creation:**

- `const instance1 = new Singleton()`: Creates the first instance of the `Singleton` class.
- `const instance2 = new Singleton()`: Attempts to create a second instance, but due to the `Singleton` pattern, it returns the same instance as `instance1`.

**Instance Comparison:**

- `console.log(instance1 === instance2)`: This logs true because both `instance1` and `instance2` refer to the same instance.

**Method Call:**

- `instance1.someMethod()`: Calls the `someMethod` on the singleton instance, logging "Singleton method called" to the console.

### Summary

- The Singleton pattern ensures that only one instance of the `Singleton` class is created.
- Any subsequent attempts to create a new instance will return the already existing instance.
- This pattern is useful for managing shared resources or coordinating actions across a system.
