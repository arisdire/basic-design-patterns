# Builder Pattern

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
