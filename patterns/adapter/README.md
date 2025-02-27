# Adapter Pattern

The Adapter pattern allows incompatible interfaces to work together by providing a wrapper that translates calls from one interface to another.

```js
// Old interface
class OldCalculator {
  constructor() {
    this.operations = function (term1, term2, operation) {
      switch (operation) {
        case "add":
          return term1 + term2;
        case "sub":
          return term1 - term2;
        default:
          return NaN;
      }
    };
  }
}

// New interface
class NewCalculator {
  add(term1, term2) {
    return term1 + term2;
  }

  sub(term1, term2) {
    return term1 - term2;
  }
}

// Adapter Class
class CalculatorAdapter {
  constructor() {
    this.newCalculator = new NewCalculator();
  }

  operations(term1, term2, operation) {
    switch (operation) {
      case "add":
        return this.newCalculator.add(term1, term2);
      case "sub":
        return this.newCalculator.sub(term1, term2);
      default:
        return NaN;
    }
  }
}
```

### Explaining the code

1. **`OldCalculator` Class:**

   - This class represents the old interface for a calculator.
   - It has a method `operations` defined within the constructor that takes two terms and an operation type (`add` or `sub`).
   - Depending on the operation type, it either adds or subtracts the terms.

2. **`NewCalculator` Class:**

   - This class represents the new interface for a calculator.
   - It has two methods: `add` and `sub`, which perform addition and subtraction respectively.

3. **`CalculatorAdapter` Class:**

   - This class acts as an adapter to bridge the old interface (`OldCalculator`) with the new interface (`NewCalculator`).
   - It creates an instance of `NewCalculator` and uses its methods within the `operations` method to perform the required calculations.
   - This allows code that uses the old interface to work with the new interface without modification.

### Usage

```js
const oldCalc = new OldCalculator();
console.log(oldCalc.operations(10, 5, "add")); // 15

const newCalc = new NewCalculator();
console.log(newCalc.add(10, 5)); // 15

const adaptedCalc = new CalculatorAdapter();
console.log(adaptedCalc.operations(10, 5, "add")); // 15
```

- Instances of `OldCalculator`, `NewCalculator`, and `CalculatorAdapter` are created.
- The `operations` method of `OldCalculator` and `CalculatorAdapter`, as well as the add method of `NewCalculator`, are demonstrated with example inputs.

### Summary

The Adapter pattern is used here to allow the `OldCalculator` interface to work with the `NewCalculator` interface by providing a `CalculatorAdapter` that translates the method calls. This pattern is useful for integrating new components into existing systems without modifying the existing code.
