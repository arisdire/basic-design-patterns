# Template Method Pattern

The Template Method pattern is a behavioral design pattern that defines the skeleton of an algorithm in a method, deferring some steps to subclasses. It allows subclasses to redefine certain steps of an algorithm without changing the algorithm's structure.

### Example

```js
class DataProcessor {
  process() {
    this.loadData();
    this.processData();
    this.saveData();
  }

  loadData() {
    throw new Error("You have to implement the method loadData!");
  }

  processData() {
    throw new Error("You have to implement the method processData!");
  }

  saveData() {
    throw new Error("You have to implement the method saveData!");
  }
}

class CSVDataProcessor extends DataProcessor {
  loadData() {
    console.log("Loading data from CSV file");
    // Load CSV data
  }

  processData() {
    console.log("Processing CSV data");
    // Process CSV data
  }

  saveData() {
    console.log("Saving processed data to CSV file");
    // Save processed data
  }
}

class JSONDataProcessor extends DataProcessor {
  loadData() {
    console.log("Loading data from JSON file");
    // Load JSON data
  }

  processData() {
    console.log("Processing JSON data");
    // Process JSON data
  }

  saveData() {
    console.log("Saving processed data to JSON file");
    // Save processed data
  }
}
```

### Explaining the code

1. **Base Class: `DataProcessor`**

   - The `DataProcessor` class contains a method `process()` which outlines the steps for processing data: `loadData()`, `processData()`, and `saveData()`.
   - Each of these methods (`loadData()`, `processData()`, and `saveData()`) throws an error, indicating that they must be implemented by subclasses.

2. **Subclass: `CSVDataProcessor`**

   - Inherits from `DataProcessor`.
   - Implements the `loadData()`, `processData()`, and `saveData()` methods specifically for CSV data.
   - Each method logs a message to the console indicating its operation.

3. **Subclass: `JSONDataProcessor`**

   - Inherits from `DataProcessor`.
   - Implements the `loadData()`, `processData()`, and `saveData()` methods specifically for JSON data.
   - Each method logs a message to the console indicating its operation.

### Usage

```js
const csvProcessor = new CSVDataProcessor();
csvProcessor.process();

const jsonProcessor = new JSONDataProcessor();
jsonProcessor.process();
```

- Instances of `CSVDataProcessor` and `JSONDataProcessor` are created.
- The `process()` method is called on each instance, which in turn calls the overridden methods (`loadData()`, `processData()`, and `saveData()`) in the respective subclasses.

### Summary

The Template Method pattern is useful when you have an algorithm that consists of several steps, and you want to allow subclasses to provide specific implementations for some of those steps while keeping the overall structure intact.
