# Factory Method Pattern

The Factory Method pattern lets a class defer instantiation to subclasses. It defines an interface for creating a single object, but lets subclasses decide which class to instantiate.

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
