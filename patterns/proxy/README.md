# Proxy Pattern

The Proxy pattern is used to control access to an object by placing a surrogate or placeholder object (the proxy) in front of the real object (the real subject).

```js
class RealSubject {
  request() {
    console.log("RealSubject: Handling request.");
  }
}

class Proxy {
  constructor(realSubject) {
    this.realSubject = realSubject;
  }

  request() {
    if (this.checkAccess()) {
      this.realSubject.request();
      this.logAccess();
    }
  }

  checkAccess() {
    console.log("Proxy: Checking access prior to firing a real request.");
    // Simulate access check
    return true;
  }

  logAccess() {
    console.log("Proxy: Logging the time of request.");
  }
}
```

### Explaining the code

1. **`RealSubject` Class:**

   - This class represents the real object that performs the actual work. It has a `request` method that logs a message indicating it is handling the request.

2. **Proxy Class:**

   - This class acts as a proxy to the `RealSubject`. It holds a reference to an instance of `RealSubject` and controls access to it.
   - The `request` method in the `Proxy` class first checks access by calling `checkAccess`. If access is granted, it forwards the request to the `RealSubject` and then logs the access by calling `logAccess`.

### Usage

```js
const realSubject = new RealSubject();
const proxy = new Proxy(realSubject);

proxy.request();
```

- An instance of `RealSubject` is created.
- An instance of `Proxy` is created, with the `RealSubject` instance passed to its constructor.
- The `request` method is called on the `Proxy` instance. This triggers the access check, forwards the request to the `RealSubject` if access is granted, and logs the access.

### Summary

The Proxy pattern is used to control access to an object. In this example, the `Proxy` class controls access to the `RealSubject` by checking access and logging the request. This pattern is useful for adding additional functionality (like access control and logging) without modifying the original class.
