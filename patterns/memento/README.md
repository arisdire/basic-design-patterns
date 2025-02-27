# Memento Pattern

The Memento pattern is used to capture and externalize an object's internal state so that it can be restored later without violating encapsulation. This is useful for implementing features like undo/redo functionality.

```js
class Memento {
  constructor(state) {
    this.state = state;
  }

  getState() {
    return this.state;
  }
}

// Originator
class Originator {
  constructor() {
    this.state = "";
  }

  setState(state) {
    this.state = state;
    console.log(`State set to: ${this.state}`);
  }

  saveStateToMemento() {
    return new Memento(this.state);
  }

  getStateFromMemento(memento) {
    this.state = memento.getState();
    console.log(`State restored to: ${this.state}`);
  }
}

// Caretaker
class Caretaker {
  constructor() {
    this.mementoList = [];
  }

  add(memento) {
    this.mementoList.push(memento);
  }

  get(index) {
    return this.mementoList[index];
  }
}
```

### Explaining the code

**Classes and Methods**

1.  **Memento**

- **Purpose:** Stores the state of the `Originator`.
- **Constructor:** Takes a `state` parameter and assigns it to the instance.
- **`getState()`:** Returns the stored state.

2. **Originator**

   - **Purpose:** Creates and stores states in `Memento` objects.
   - **Constructor:** Initializes the `state` to an empty string.
   - **`setState(state)`:** Sets the current state and logs it.
   - **`saveStateToMemento()`:** Creates a new Memento with the current state.
   - **`getStateFromMemento(memento)`:** Restores the state from a given `Memento` and logs it.

3. **Caretaker**

   - **Purpose:** Manages the `Memento` objects.
   - **Constructor:** Initializes an empty list to store `Memento` objects.
   - **add(memento):** Adds a `Memento` to the list.
   - **get(index):** Retrieves a `Memento` from the list by index.

# Usage

```js
const originator = new Originator();
const caretaker = new Caretaker();

originator.setState("State #1");
originator.setState("State #2");
caretaker.add(originator.saveStateToMemento());

originator.setState("State #3");
caretaker.add(originator.saveStateToMemento());

originator.setState("State #4");

console.log("Current State:", originator.state);
originator.getStateFromMemento(caretaker.get(0));
console.log("First saved State:", originator.state);
originator.getStateFromMemento(caretaker.get(1));
console.log("Second saved State:", originator.state);
```

- Create instances of `Originator` and `Caretaker`.
- Set various states in the `Originator`.
- Save states to `Memento` objects and store them in the `Caretaker`.
- Restore states from `Memento` objects using the `Caretaker`.

### Summary

The `Originator` class can save its state to a `Memento` object and restore it later. The `Caretaker` class manages these `Memento` objects, allowing the `Originator` to revert to previous states. The Memento pattern is useful for scenarios where you need to implement undo/redo functionality.
