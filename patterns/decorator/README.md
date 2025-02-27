# Decorator Pattern

The Decorator pattern allows behavior to be added to individual objects, dynamically, without affecting the behavior of other objects from the same class.

```js
// Base component
class Coffee {
  cost() {
    return 5;
  }
}

// Decorator base class
class CoffeeDecorator {
  constructor(coffee) {
    this.coffee = coffee;
  }

  cost() {
    return this.coffee.cost();
  }
}

// Concrete Decorators
class MilkDecorator extends CoffeeDecorator {
  cost() {
    return this.coffee.cost() + 1;
  }
}

class SugarDecorator extends CoffeeDecorator {
  cost() {
    return this.coffee.cost() + 0.5;
  }
}
```

### Explaining the code

1. **Base Component:** The `Coffee` class represents the base component with a `cost` method that returns the base price of a coffee, which is 5.
2. **Decorator Base Class:** The `CoffeeDecorator` class is a base decorator class that takes a `coffee` object and delegates the cost method to it. This class is designed to be extended by concrete decorators.
3. **Concrete Decorators:**

   - **`MilkDecorator`**
     - The `MilkDecorator` class extends `CoffeeDecorator` and adds the cost of milk (1) to the base coffee cost.
   - **`SugarDecorator`**
     - The `SugarDecorator` class extends `CoffeeDecorator` and adds the cost of sugar (0.5) to the base coffee cost.

### Usage

```js
let myCoffee = new Coffee();
console.log(myCoffee.cost()); // 5

myCoffee = new MilkDecorator(myCoffee);
console.log(myCoffee.cost()); // 6

myCoffee = new SugarDecorator(myCoffee);
console.log(myCoffee.cost()); // 6.5
```

- Initially, `myCoffee` is a plain `Coffee` object with a cost of 5.
- Then, `myCoffee` is wrapped with a `MilkDecorator`, increasing the cost to 6.
- Finally, `myCoffee` is wrapped with a `SugarDecorator`, increasing the cost to 6.5.

### Summary

The Decorator pattern is used to dynamically add additional costs (milk and sugar) to a base coffee object. This pattern is useful for extending the functionality of objects in a flexible and reusable way.
