# Themer.js

Spice up your app with themes. Themer.js features include:

- Automatic night/day theme switching
- System [prefers-color-scheme](https://developer.mozilla.org/en-US/docs/Web/CSS/@media/prefers-color-scheme) support
- Android [meta theme-color](https://developers.google.com/web/updates/2014/11/Support-for-theme-color-in-Chrome-39-for-Android) support
- Custom themes
- Manual control over everything

## Demo

[https://themer.js.kmr.io](https://themer.js.kmr.io)

## <a name="quick-start"></a>Quick Start

### Install

```
# using yarn
$ yarn add themer.js

# using npm
$ npm install themer.js
```

### Define the `light` and `dark` themes

To use the `auto` or `system` themes, you must define a `light` and `dark` [Theme object](#theme).

```
import Themer from "themer.js";

const config = {
  "light": {
    "styles": {
      "--app-background-color": "#f1f1f1",
      "--primary-text-color": "#555"
    }
  },
  "dark": {
    "styles": {
      "--app-background-color": "#242835",
      "--primary-text-color": "#f1f1f1"
    }
  }
}

// instantiate Themer.js
const themer = new Themer(config);
```

### Setting a theme

```
import Themer from "themer.js";
import { light, dark } from "./themes/index.js";

const themer = new Themer({ light, dark });

// set theme to dark
themer.setTheme(dark);

// set theme to auto
themer.setAuto();

// set theme to system
themer.setSystem();
```

### Setting a custom theme

Pass a valid [Theme `object`](#theme) to [setTheme()](#setTheme).

```
import Themer from "themer.js";

const custom = {
  "styles": {
    "--app-background-color": "#f1f1f1",
    "--primary-text-color": "#555"
  }
};

const themer = new Themer();

themer.setTheme(custom);
```

## <a name="api"></a>API

### <a name="themer"></a>Themer(config)

- **Arguments:**
  - `{Object} config`
- **Details:** Instantiate Themer.js.
- **Usage:**

  ```
  import { light, dark } from "./themes/index.js";

  const config = {
    light,
    dark,
    debug: true,
    onUpdate: (theme) => console.log(theme)
  };

  const themer = new Themer(config);
  ```

- See also: [Config object](#config)

### <a name="setAuto"></a>Themer.setAuto()

- **Details:** Sets the active theme to `light` during the day and `dark` during the night.
- **Restrictions:**
  - `light` and `dark` themes must be defined.
  - Requires user geolocation consent.
- **Usage:**

  ```
  Themer.setAuto();
  ```

### <a name="setSystem"></a>Themer.setSystem()

- **Details:** Sets the active theme to `system`.
- **Restriction:**
  - `light` and `dark` themes must be defined.
  - The browser must support [prefers-color-scheme](https://caniuse.com/#feat=prefers-color-scheme).
- **Usage:**

  ```
  Themer.setSystem();
  ```

  **See also:** [Themer.systemThemeSupport()](#systemThemeSupport)

### <a name="setTheme"></a>Themer.setTheme( theme )

- **Arguments:**
  - `{Object | string} theme`
- **Details:** Sets the active theme.
- **Usage:**

  ```
  const dark = {
    "android": "#242835",
    "styles": {
      "--app-background-color": "#242835"
    }
  };

  Themer.setTheme(dark);
  ```

- **See also:** [Theme `object`](#theme)

### <a name="systemThemeSupport"></a>Themer.systemThemeSupport()

- **Details:** Helper function to determine browser support for the `system` theme.
- **Returns:** `boolean`
- **Usage:**

  ```
  // Chrome 76, Firefox 67, Safari 12.1
  Themer.systemThemeSupport();
  ↳ true

  // unsupported browsers
  Themer.systemThemeSupport();
  ↳ false
  ```

- See also: [prefers-color-scheme](https://caniuse.com/#feat=prefers-color-scheme)

### <a name="config"></a>Config `object`

| Key        | Type       | Description                                       |
| ---------- | ---------- | ------------------------------------------------- |
| `debug`    | `boolean`  | Log debug console statements.                     |
| `onUpdate` | `function` | A callback function that returns the set `theme`. |
| `light`    | `object`   | The `dark` theme.                                 |
| `dark`     | `object`   | The `light` theme.                                |

**Example:**

```
{
  debug: true,
  onUpdate: (theme) => console.log(theme),
  "light": {
    "styles": {
      "--app-background-color": "#f1f1f1",
      "--primary-text-color": "#555"
    }
  },
  "dark": {
    "styles": {
      "--app-background-color": "#242835",
      "--primary-text-color": "#f1f1f1"
    }
  }
}
```

### <a name="theme"></a>Theme `object`

| Key       | Type     | Description                                                                                                                      |
| --------- | -------- | -------------------------------------------------------------------------------------------------------------------------------- |
| `android` | `string` | Sets the [meta theme-color](https://developers.google.com/web/updates/2014/11/Support-for-theme-color-in-Chrome-39-for-Android). |
| `styles`  | `object` | The theme CSS variables.                                                                                                         |

**Example:**

```
{
  "android": "#f1f1f1",
  "styles": {
    "--app-background-color": "#f1f1f1",
    "--primary-text-color": "#555"
  }
}
```

Use the CSS variables anywhere in your CSS and it will update in real time to the active theme.

```
html {
  background-color: var(--app-background-color);
  color: var(--primary-text-color);
}
```
