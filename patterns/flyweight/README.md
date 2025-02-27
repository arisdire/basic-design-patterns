# Flyweight Pattern

The Flyweight pattern is used to minimize memory usage by sharing as much data as possible with similar objects.

```js
class Flyweight {
  constructor(make, model, processor) {
    this.make = make;
    this.model = model;
    this.processor = processor;
  }
}

class FlyweightFactory {
  constructor() {
    this.flyweights = {};
  }

  get(make, model, processor) {
    const key = `${make}-${model}-${processor}`;
    if (!this.flyweights[key]) {
      this.flyweights[key] = new Flyweight(make, model, processor);
    }
    return this.flyweights[key];
  }

  getCount() {
    return Object.keys(this.flyweights).length;
  }
}

class Computer {
  constructor(make, model, processor, memory, tag) {
    this.flyweight = FlyweightFactory.get(make, model, processor);
    this.memory = memory;
    this.tag = tag;
  }
}

class ComputerCollection {
  constructor() {
    this.computers = {};
    this.count = 0;
  }

  add(make, model, processor, memory, tag) {
    this.computers[tag] = new Computer(make, model, processor, memory, tag);
    this.count++;
  }

  get(tag) {
    return this.computers[tag];
  }

  getCount() {
    return this.count;
  }
}
```

### Explaining the code

1. **`Flyweight`:**

   - Represents the shared part of the object. In this case, it includes`make`, `model`, and `processor`.
   - Constructor initializes these properties.

2. **`FlyweightFactory`:**

   - Manages the flyweight objects.
   - Contains a method `get` to retrieve an existing flyweight or create a new one if it doesn't exist.
   - `getCount` method returns the number of unique flyweights created.

3. **`Computer`:**

   - Represents the full object, which includes both shared (flyweight) and unique parts.
   - Constructor initializes the flyweight part using `FlyweightFactory.get` and also initializes unique properties like `memory` and `tag`.

4. **`ComputerCollection`:**

   - Manages a collection of `Computer` objects.
   - `add` method adds a new computer to the collection.
   - `get` method retrieves a computer by its tag.
   - `getCount` method returns the number of computers in the collection.

### Usage

```js
const factory = new FlyweightFactory();
const computers = new ComputerCollection();

computers.add("Dell", "XPS", "Intel", "16GB", "1");
computers.add("Dell", "XPS", "Intel", "8GB", "2");
computers.add("HP", "Envy", "AMD", "16GB", "3");
computers.add("HP", "Envy", "AMD", "8GB", "4");

console.log(`Computers: ${computers.getCount()}`);
console.log(`Flyweights: ${factory.getCount()}`);
```

- A `FlyweightFactory` instance is created to manage flyweights.
- A `ComputerCollection` instance is created to manage computers.
- Several computers are added to the collection with varying memory and tags but shared make, model, and processor.
- The total number of computers and flyweights are logged to the console.

### Summary

The Flyweight pattern is effectively used here to reduce memory usage by sharing common data (make, model, processor) among multiple `Computer` objects. The `FlyweightFactory` ensures that only one instance of each unique combination of make, model, and processor is created and reused. This pattern is particularly useful when dealing with a large number of objects that share common data.
