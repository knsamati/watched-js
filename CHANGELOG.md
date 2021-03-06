# Changelog

## v0.35.0

### Changes

- Added `SetResultError` to set cache results in a different way. For more infos, see the code documentation.
- Added IPTV category property and default filter values
- Removed the `@watchedcom/create` package
- Removed the `watched-sdk` command line tool
- Added experimental `FetchAgent`

## v0.34.0

### Changes

- Dropping legacy Node.js versions (=> 12.9 is now required)
- Added similar item system for items. See the `similarItem` property. Similar items will be displayed as horizontal lists below movie, series or channel items.
- Created `toast` task to display toast messages inside the app (see `ctx.toast`)
- Created `notification` task to display notifications with various options inside the app (see `ctx.notification`). Notifications can be displayed once every 30 minute per addon. You can set the `url` property to open an URL when the user clicks on the notification. WATCHED sharing URL's are handled internally, so you can promote for example an item or addon.
- Various bugfixes and improvments

### Upgrade instructions

Edit your `tsconfig.json` and replace

```json
  "target": "es5",
```

with

```json
  "target": "es2019",
  "lib": ["es2020"],
  "moduleResolution": "node",
```

## v0.31.0

### Changes

- Created `CHANGELOG.md`

### Legacy

- The `watched-sdk` command line tool will be legacy starting with v0.32
- The [`@watchedcom/create`](packages/create) command line tool is printing a legacy message
- The `testAddon` function in [`@watchedcom/test`](packages/test) is printing a legacy message when it's used

### Upgrade instructions

Since the `watched-sdk` command is legacy, you can't export your addons anymore.

- Install `ts-node-dev`:

  ```shell
  npm install --save-dev ts-node-dev
  ```

- **`package.json`** (change the `start` and `develop` scripts)

  ```json
  {
    "scripts": {
      "build": "tsc",
      "start": "node .",
      "develop": "ts-node-dev --transpileOnly src",
      "test": "jest"
    }
  }
  ```

- **`src/index.ts`**

  ```ts
  import { runCli } from "@watchedcom/sdk";

  // Your code here

  runCli([yourAddon, anotherAddon]);
  ```
