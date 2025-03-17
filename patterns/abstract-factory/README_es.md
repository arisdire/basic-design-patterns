# Diseño Abstract Factory

El diseño Abstract Factory proporciona una interfaz para crear familias de objetos relacionados o dependientes sin especificar sus clases concretas.

### Ejemplo

```js
// Abstract Product
class Button {
  render() {
    throw new Error("Este mensaje debe ser sobreescrito!");
  }
}
```

La clase `Button` es un producto abstracto. Define un método `render` que debe ser sobreescrito por cualquier producto concreto que extienda esta clase.

```js
// Concrete Product
class WindowsButton extends Button {
  render() {
    console.log("Representar un botón en estilo Windows.");
  }
}

class MacOSButton extends Button {
  render() {
    console.log("Representar un botón en estilo MacOS.");
  }
}
```

`WindowsButton` y `MacOSButton` son productos concretos que extienden la clase `Button`. Proporcionan implementaciones específicas del método 'render'.

```js
// Abstract Factory
class GUIFactory {
  createButton() {
    throw new Error("Este mensaje debe ser sobreescrito!");
  }
}
```

La clase `GUIFactory` es una fábrica abstracta. Define un método `createButton` que debe ser anulado por cualquier fábrica concreta que extienda esta clase.

```js
// Concrete Factory
class WindowsFactory extends GUIFactory {
  createButton() {
    return new WindowsButton();
  }
}

class MacOSFactory extends GUIFactory {
  createButton() {
    return new MacOSButton();
  }
}
```

`WindowsFactory` y `MacOSFactory` son fabricas concretas que extienden la clase `GUIFactory`. Proporcionan implementaciones específicas del método `createButton`, devolviendo instancias de `WindowsButton` y `MacOSButton`, respectivamente.

```js
// Client Code
function createUI(factory) {
  const button = factory.createButton();
  button.render();
}
```

La función `createUI` function es el código del cliente que utiliza una fábrica para crear y renderizar un botón. Toma una fábrica como argumento, llama al método `createButton` en la fábrica para obtener un botón y luego llama al método `render` en el botón.

### Uso

```js
const windowsFactory = new WindowsFactory();
createUI(windowsFactory);

const macFactory = new MacOSFactory();
createUI(macFactory);
```

### Resumen

Aquí, creamos instancias de `WindowsFactory` y `MacOSFactory` y las pasamos a la función `createUI`. Esto demuestra cómo el código del cliente puede trabajar con diferentes fábricas para crear y renderizar botones en diferentes estilos. El patrón Abstract Factory permite desacoplar el código del cliente de las clases específicas de objetos que necesita crear, lo que promueve la flexibilidad y la escalabilidad.
