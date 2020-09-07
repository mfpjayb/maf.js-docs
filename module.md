# Module

Every component of an application is a part of a module.
This is a way to group components, plugins and other part of application that are related to each other.

## Module root component

Every module has a root component which will be displayed when a module is moounted on the dom tree.

```javascript
import { Module } from 'maf.js';
import App from './App';

new Module({
    component: App
});
```

In this example, `App` is the root component.

## Mount to dom tree

Module must be mounted to the dom tee first before we can interact with its components.

```javascript
import { Module } from 'maf.js';
import App from './App';

const module = new Module({
    component: App
});

module.mount('#app', true);
```

On the last line of the code above, the first argument is the selector of the element where the module will be mounted.
In the second parameter, `true` means the element will be replaced with the root element of the module and `false` will only append the root element of the module inside the selected element.

## Include a plugin

Including a plugin in a module must be called first before the module is mounted.
Here's an example on how to use a plugin:

```javascript
import { Module, Store } from 'maf.js';
import App from './App';

const module = new Module({
    component: App
});

module.plugin(Store, {});

module.mount('#app', true);
```

The first argument for the `plugin` method call is the plugin itself and second parameter are some data for the plugin.

