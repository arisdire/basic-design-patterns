# Basic Design Patterns

Basic design pattern examples in JavaScript.

## Table of Contents

1. [Builder](#builder-pattern)
1. [Facade](#facade-pattern)
1. [Factory Method](#factory-method-pattern)
1. [Protoype](#prototype-pattern)
1. [Singleton](#singleton-pattern)

## Builder Pattern

The Builder pattern separates the construction of a complex object from its representation. This allows the same construction process to create different representations of the object.

```js
// The Car class represents a car with various properties such as make, model, year, color, and engine. It uses a builder object to initialize these properties.
class Car {
  constructor(builder) {
    this.make = builder.make;
    this.model = builder.model;
    this.year = builder.year;
    this.color = builder.color;
    this.engine = builder.engine;
  }

  // Returns a string representation of the car
  toString() {
    return `${this.year} ${this.make} ${this.model} in ${this.color} with a ${this.engine} engine`;
  }
}
```

The `CarBuilder` class helps in building a `Car` object step by step. It allows setting various properties of the car and then building the final `Car` object.

```js
// CarBuilder class helps in building a Car object step by step
class CarBuilder {
  constructor(make, model) {
    this.make = make;
    this.model = model;
  }

  // Sets the year of the car
  setYear(year) {
    this.year = year;
    return this;
  }

  // Sets the color of the car
  setColor(color) {
    this.color = color;
    return this;
  }

  // Sets the engine type of the car
  setEngine(engine) {
    this.engine = engine;
    return this;
  }

  // Builds and returns a Car object
  build() {
    return new Car(this);
  }
}
```

This example demonstrates how to use the `CarBuilder` class to create a `Car` object.

```js
// Usage example
const car = new CarBuilder("Toyota", "Camry")
  .setYear(2021) // Setting the year
  .setColor("Red") // Setting the color
  .setEngine("V6") // Setting the engine type
  .build(); // Building the car

// Output the car details
console.log(car.toString());
```

### Explaining the code

1. **Fluent Interface:** The `CarBuilder` class uses a fluent interface, allowing method chaining. Each setter method returns the builder object itself (`this`), enabling chaining multiple method calls in a single statement.
2. **Separation of Concerns:** The builder pattern separates the construction of a complex object (`Car`) from its representation, allowing the same construction process to create various representations.
3. **Immutability:** Once a `Car` object is created, its properties are immutable (cannot be changed), ensuring the integrity of the object.

The Builder pattern is useful for constructing complex objects with many optional parameters.

<sup>[Back to top](#table-of-contents)</sup>

## Facade Pattern

The Facade pattern provides a unified interface to a set of interfaces in a subsystem. It defines a higher-level interface that makes the subsystem easier to use.

```js
// Subsystem 1: CPU class with methods to freeze, jump to a position, and execute instructions
class CPU {
  // Freezes the CPU
  freeze() {
    console.log("Freezing CPU...");
  }

  // Jumps to a specific position in memory
  jump(position) {
    console.log(`Jumping to position ${position}...`);
  }

  // Executes instructions
  execute() {
    console.log("Executing instructions...");
  }
}

// Subsystem 2: Memory class with a method to load data at a specific position
class Memory {
  // Loads data into a specific position in memory
  load(position, data) {
    console.log(`Loading data '${data}' at position ${position}...`);
  }
}

// Subsystem 3: HardDrive class with a method to read data from a specific LBA (Logical Block Addressing)
class HardDrive {
  // Reads data from a specific LBA and returns the data
  read(lba, size) {
    console.log(`Reading ${size} bytes from LBA ${lba}...`);
    return "data";
  }
}

// Facade: ComputerFacade class to simplify the interaction with the subsystems
class ComputerFacade {
  constructor() {
    // Initialize subsystems
    this.cpu = new CPU();
    this.memory = new Memory();
    this.hardDrive = new HardDrive();
  }

  // Method to start the computer by coordinating the subsystems
  start() {
    // Freeze the CPU
    this.cpu.freeze();
    // Load data from the hard drive into memory
    this.memory.load(0, this.hardDrive.read(0, 1024));
    // Jump to the start position in memory
    this.cpu.jump(0);
    // Execute instructions
    this.cpu.execute();
  }
}

// Client code: Creating an instance of ComputerFacade and starting the computer
const computer = new ComputerFacade();
computer.start();
```

### Explaining the code

**Subsystem Classes:**

- **`CPU`:** Represents the CPU with methods to freeze, jump to a memory position, and execute instructions.
- **`Memory`:** Represents the memory with a method to load data at a specific position.
- **`HardDrive`:** Represents the hard drive with a method to read data from a specific Logical Block Addressing (LBA).

**Facade Class:**

- **ComputerFacade:** Simplifies the interaction with the subsystems by providing a higher-level interface. It initializes instances of the `CPU`, `Memory`, and `HardDrive` classes and provides a `start` method to coordinate their actions.

**Client Code:**

- Creates an instance of `ComputerFacade` and calls the `start` method to start the computer, which internally coordinates the actions of the `CPU`, `Memory`, and `HardDrive` subsystems.

<sup>[Back to top](#table-of-contents)</sup>

## Factory Method Pattern

Factory Method lets a class defer instantiation to subclasses. It defines an interface for creating a single object, but lets subclasses decide which class to instantiate.

```js
// Class for Car
class Car {
  constructor({ doors = 4, state = "brand new", color = "silver" } = {}) {
    this.doors = doors;
    this.state = state;
    this.color = color;
  }
}
```

The `Car` class initializes a car object with properties `doors`, `state`, and `color`. Default values are provided using destructuring and default parameters.

```js
// Class for Truck
class Truck {
  constructor({ doors = 2, state = "used", color = "blue" } = {}) {
    this.doors = doors;
    this.state = state;
    this.color = color;
  }
}
```

Similar to the `Car` class, the `Truck` class initializes a truck object with properties `doors`, `state`, and `color`. Default values are also provided using destructuring and default parameters.

```js
// Factory class
class VehicleFactory {
  // Method to create a vehicle based on the provided options
  createVehicle(options) {
    switch (options.vehicleType) {
      // If vehicleType is "car", create a new Car
      case "car":
        return new Car(options);
      // If vehicleType is "truck", create a new Truck
      case "truck":
        return new Truck(options);
      // If vehicleType is not recognized, return null
      default:
        return null;
    }
  }
}
```

### Explaining the code

- The `createVehicle` method is added to the `VehicleFactory` class.
- It takes an options object as an argument and uses a switch statement to determine which type of vehicle to create based on the `vehicleType` property.
- If `vehicleType` is "car", it creates and returns a new `Car` object.
- If `vehicleType` is "truck", it creates and returns a new `Truck` object.
- If `vehicleType` is not recognized, it returns `null`.

### Usage

```js
const factory = new VehicleFactory();

// Create a car with specified options
const car = factory.createVehicle({
  vehicleType: "car",
  doors: 4,
  color: "red",
  state: "new",
});

// Create a truck with specified options
const truck = factory.createVehicle({
  vehicleType: "truck",
  doors: 2,
  color: "black",
  state: "used",
});
```

### Summary

- An instance of `VehicleFactory` is created.
- The `createVehicle` method is called with specific options to create a `Car` and a `Truck`.
- The created car and truck objects have the specified properties.

<sup>[Back to top](#table-of-contents)</sup>

## Prototype Pattern

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

<sup>[Back to top](#table-of-contents)</sup>

## Singleton Pattern

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

<sup>[Back to top](#table-of-contents)</sup>
