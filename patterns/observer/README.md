# Observer Pattern

The Observer pattern is a behavioral design pattern where an object (the subject) maintains a list of its dependents (observers) and notifies them of any state changes, usually by calling one of their methods.

```js
// Subject
class Subject {
  constructor() {
    this.observers = [];
  }

  subscribe(observer) {
    this.observers.push(observer);
  }

  unsubscribe(observer) {
    this.observers = this.observers.filter((obs) => obs !== observer);
  }

  notify(data) {
    this.observers.forEach((observer) => observer.update(data));
  }
}

// Observer
class Observer {
  update(data) {
    console.log(`Observer received data: ${data}`);
  }
}
```

### Explaining the code

**Classes and Methods**

1. **Subject Class**

   - **Constructor:** Initializes an empty array `observers` to keep track of the observers.
   - **`subscribe(observer)`:** Adds an observer to the `observers` array.
   - **`unsubscribe(observer)`:** Removes an observer from the `observers` array by filtering it out.
   - **`notify(data)`:** Calls the `update` method on each observer in the `observers` array, passing the data to them.

2. **Observer Class**

   - **`update(data)`:** A method that logs the received data to the console. This method is intended to be overridden by concrete observer implementations.

### Usage

```js
const subject = new Subject();

const observer1 = new Observer();
const observer2 = new Observer();

subject.subscribe(observer1);
subject.subscribe(observer2);

subject.notify("Hello Observers!"); // Both observers will log the data

subject.unsubscribe(observer1);

subject.notify("Hello again!"); // Only observer2 will log the data
```

- **Creating Instances:**
  - A `Subject` instance is created.
  - Two `Observer` instances are created.
- **Subscribing Observers:**
  - Both observers are subscribed to the subject.
- **Notifying Observers:**
  - The subject notifies all subscribed observers with the message "Hello Observers!".
  - The first observer is unsubscribed.
  - The subject notifies the remaining observers with the message "Hello again!".

### Summary

This code demonstrates the Observer pattern where a `Subject` can notify multiple `Observer` instances about changes. Observers can subscribe to or unsubscribe from the subject. When the subject's state changes, it notifies all subscribed observers by calling their `update` method. This pattern is useful for implementing distributed event handling systems.
