# Bridge Pattern

The Bridge pattern is used to separate an abstraction from its implementation, allowing them to vary independently. Here's a breakdown of the key components:

### Example

```js
// Abstraction
class RemoteControl {
  constructor(device) {
    this.device = device;
  }

  togglePower() {
    if (this.device.isEnabled()) {
      this.device.disable();
    } else {
      this.device.enable();
    }
  }

  volumeUp() {
    this.device.setVolume(this.device.getVolume() + 10);
  }

  volumeDown() {
    this.device.setVolume(this.device.getVolume() - 10);
  }
}

// Refined Abstraction
class AdvancedRemoteControl extends RemoteControl {
  mute() {
    this.device.setVolume(0);
  }
}

// Implementor
class Device {
  constructor() {
    this.volume = 50;
    this.enabled = false;
  }

  isEnabled() {
    return this.enabled;
  }

  enable() {
    this.enabled = true;
  }

  disable() {
    this.enabled = false;
  }

  getVolume() {
    return this.volume;
  }

  setVolume(volume) {
    this.volume = volume;
  }
}

// Concrete Implementor
class TV extends Device {
  constructor() {
    super();
  }

  // Additional TV-specific methods
}

class Radio extends Device {
  constructor() {
    super();
  }

  // Additional Radio-specific methods
}
```

### Explaining the code

1. **Abstraction:** The `RemoteControl` class acts as the abstraction. It defines the interface for controlling devices but delegates the actual work to the `device` object.
2. **Refined Abstraction:** The `AdvancedRemoteControl` class extends `RemoteControl` and adds more functionality, such as the `mute` method.
3. **Implementor:** The `Device` class defines the interface for all concrete devices. It includes methods to enable/disable the device and get/set the volume.
4. **Concrete Implementors:** The `TV` and `Radio` classes extend the `Device` class and can have additional methods specific to each device type.

### Usage

```js
const tv = new TV();
const remote = new RemoteControl(tv);

remote.togglePower();
console.log(tv.isEnabled()); // true

remote.volumeUp();
console.log(tv.getVolume()); // 60

const radio = new Radio();
const advancedRemote = new AdvancedRemoteControl(radio);

advancedRemote.togglePower();
console.log(radio.isEnabled()); // true

advancedRemote.mute();
console.log(radio.getVolume()); // 0
```

### Summary

This pattern decouples an abstraction (`RemoteControl`) from its implementation (`Device`) so that the two can vary independently.

- `RemoteControl` is the abstraction that interacts with a `Device`.
- `AdvancedRemoteControl` is a refined abstraction that adds more functionality.
- `Device` is the implementor that defines the interface for concrete devices.
- `TV` and `Radio` are concrete implementors that extend `Device`.

The Bridge pattern allows you to add new remote controls or devices without changing the existing code, promoting flexibility and scalability.
