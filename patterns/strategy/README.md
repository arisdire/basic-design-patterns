# Strategy

The Strategy pattern allows you to define a family of algorithms, encapsulate each one as a class, and make them interchangeable. This pattern lets the algorithm vary independently from the clients that use it.

```js
// Strategy interface
class Strategy {
  execute(a, b) {
    throw new Error("This method should be overridden!");
  }
}

// Concrete strategies
class AddStrategy extends Strategy {
  execute(a, b) {
    return a + b;
  }
}

class SubtractStrategy extends Strategy {
  execute(a, b) {
    return a - b;
  }
}

class MultiplyStrategy extends Strategy {
  execute(a, b) {
    return a * b;
  }
}

class DivideStrategy extends Strategy {
  execute(a, b) {
    if (b === 0) {
      throw new Error("Division by zero!");
    }
    return a / b;
  }
}

// Context
class Calculator {
  constructor(strategy) {
    this.strategy = strategy;
  }

  setStrategy(strategy) {
    this.strategy = strategy;
  }

  executeStrategy(a, b) {
    return this.strategy.execute(a, b);
  }
}
```

### Explaining the code

1. **Strategy Interface:** The `Strategy` class defines an interface with an `execute` method that must be overridden by concrete strategy classes.
2. **Concrete Strategies:** These classes extend the `Strategy` class and implement the `execute` method with specific algorithms.
3. **Context:** The `Calculator` class acts as the context that uses a Strategy object.

   - **`constructor(strategy)`:** Initializes the calculator with a specific strategy.
   - **`setStrategy(strategy)`:** Allows changing the strategy at runtime.
   - **`executeStrategy(a, b)`:** Executes the current strategy's algorithm.

### Usage

```js
const calculator = new Calculator(new AddStrategy());
console.log(calculator.executeStrategy(5, 3)); // Output:

calculator.setStrategy(new SubtractStrategy());
console.log(calculator.executeStrategy(5, 3)); // Output: 2

calculator.setStrategy(new MultiplyStrategy());
console.log(calculator.executeStrategy(5, 3)); // Output: 15

calculator.setStrategy(new DivideStrategy());
console.log(calculator.executeStrategy(6, 3)); // Output: 2
```

### Summary

The code implements the Strategy pattern to perform different arithmetic operations (addition, subtraction, multiplication, division) using interchangeable strategy objects. The `Calculator` class uses these strategies to execute the desired operation, allowing for flexible and dynamic changes to the algorithm used at runtime.
