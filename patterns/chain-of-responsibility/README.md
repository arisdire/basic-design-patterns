# Chain-of-Responsibility Pattern

The Chain-of-Responsibility pattern allows for flexible and scalable handling of requests. The following code implements a simple example of the pattern in JavaScript to simulate an ATM dispensing different denominations of bills

### Example

```js
class Request {
  constructor(amount) {
    this.amount = amount;
  }

  get(bill) {
    let count = Math.floor(this.amount / bill);
    this.amount -= count * bill;
    console.log(`Dispense ${count} $${bill} bills`);
  }
}

class Dispenser {
  constructor(bill, next) {
    this.bill = bill;
    this.next = next;
  }

  handle(request) {
    request.get(this.bill);
    if (this.next) {
      this.next.handle(request);
    }
  }
}
```

### Explaining the code

**Classes and Methods**

1. **Request Class:**

   - **Constructor:** Initializes the `amount` of money requested.
   - **`get(bill)`:** Calculates how many bills of a certain denomination can be dispensed from the current amount. It then reduces the amount by the total value of the dispensed bills and logs the number of bills dispensed.

2. **Dispenser Class:**
   - **Constructor:** Initializes the dispenser with a specific bill denomination (`bill`) and a reference to the next dispenser in the chain (next).
   - **`handle(request)`:** Dispenses the bills of its denomination by calling `request.get(this.bill)`. If there is a next dispenser in the chain, it passes the request to the next dispenser.

**Chain of Responsibility**

The dispensers are linked in a chain where each dispenser handles a specific denomination:

- `dispenser5` handles $5 bills.
- `dispenser10` handles $10 bills.
- `dispenser20` handles $20 bills.
- `dispenser50` handles $50 bills.

**Execution Flow**

1. A `Request` object is created with an amount of 135.
2. The `handle` method of `dispenser5` is called with the request.
3. `dispenser5` dispenses as many $5 bills as possible and passes the remaining amount to `dispenser10`.
4. `dispenser10` dispenses as many $10 bills as possible and passes the remaining amount to `dispenser20`.
5. `dispenser20` dispenses as many $20 bills as possible and passes the remaining amount to `dispenser50`.
6. `dispenser50` dispenses as many $50 bills as possible.

### Usage

```js
const dispenser50 = new Dispenser(50, null);
const dispenser20 = new Dispenser(20, dispenser50);
const dispenser10 = new Dispenser(10, dispenser20);
const dispenser5 = new Dispenser(5, dispenser10);

const request = new Request(135);
dispenser5.handle(request);
```

### Output

The console will display the number of bills dispensed for each denomination:

```
Dispense 1 $5 bills
Dispense 1 $10 bills
Dispense 1 $20 bills
Dispense 1 $50 bills
```

### Summary

The Chain-of-Responsibility pattern used here creates a chain of dispensers that handle different denominations of bills. Each dispenser processes the request for its denomination and passes the remaining amount to the next dispenser in the chain. This pattern allows for flexible and scalable handling of requests.
