# Composite Pattern

The Composite pattern allows you to compose objects into tree structures to represent part-whole hierarchies. It lets clients treat individual objects and compositions of objects uniformly.

```js
// Component
class Component {
  constructor(name) {
    this.name = name;
  }

  add(component) {
    throw new Error("Method not implemented");
  }

  remove(component) {
    throw new Error("Method not implemented");
  }

  display(depth) {
    throw new Error("Method not implemented");
  }
}

// Leaf
class Leaf extends Component {
  constructor(name) {
    super(name);
  }

  add(component) {
    console.log("Cannot add to a leaf");
  }

  remove(component) {
    console.log("Cannot remove from a leaf");
  }

  display(depth) {
    console.log("-".repeat(depth) + this.name);
  }
}

// Composite
class Composite extends Component {
  constructor(name) {
    super(name);
    this.children = [];
  }

  add(component) {
    this.children.push(component);
  }

  remove(component) {
    const index = this.children.indexOf(component);
    if (index !== -1) {
      this.children.splice(index, 1);
    }
  }

  display(depth) {
    console.log("-".repeat(depth) + this.name);
    for (const child of this.children) {
      child.display(depth + 2);
    }
  }
}
```

### Explaining the code

1. **Component Class:**

   - This is an abstract class that defines the interface for all objects in the composition.
   - It has methods `add`, `remove`, and `display` which are meant to be overridden by subclasses.
   - By default, these methods throw an error indicating they are not implemented.

2. **Leaf Class:**

   - This class represents the leaf objects in the composition. A leaf has no children.
   - It overrides the `add` and `remove` methods to indicate that these operations are not supported.
   - The `display` method prints the name of the leaf with a specific depth.

3. **Composite Class:**

   - This class represents the composite objects that can have children.
   - It maintains a list of child components.
   - The `add` method adds a child component to the list.
   - The `remove` method removes a child component from the list.
   - The `display` method prints the name of the composite and then recursively calls `display` on its children, increasing the depth.

### Usage

```js
const root = new Composite("root");
const branch1 = new Composite("branch1");
const branch2 = new Composite("branch2");
const leaf1 = new Leaf("leaf1");
const leaf2 = new Leaf("leaf2");
const leaf3 = new Leaf("leaf3");

root.add(branch1);
root.add(branch2);
branch1.add(leaf1);
branch2.add(leaf2);
branch2.add(leaf3);

root.display(1);
```

- A tree structure is created with a root composite, two branch composites, and three leaf nodes.
- The `add` method is used to build the tree structure.
- The `display` method is called on the root to print the entire structure.

### Output

The `display` method will produce the following output:

```
-root
--branch1
----leaf1
--branch2
----leaf2
----leaf3
```

This output shows the hierarchical structure of the composite tree, with each level of depth indicated by a series of dashes.

### Summary

The tree is built by adding branches and leaves to the appropriate composites, and the structure is displayed starting from the root with a depth of 1. The Composite pattern is useful for representing hierarchical structures and allows for flexible and uniform treatment of individual objects and compositions.
