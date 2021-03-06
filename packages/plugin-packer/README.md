kintone-plugin-packer
====

[kintone plugin package.sh](https://github.com/kintone-samples/plugin-samples) in JavaScript

[![npm version](https://badge.fury.io/js/%40kintone%2Fplugin-packer.svg)](https://badge.fury.io/js/%40kintone%2Fplugin-packer)

It's written in pure JavaScript, so

- The CLI works with Node.js in Mac/Windows/Linux
- [The web page](https://kintone.github.io/plugin-packer/) works in any modern browsers
- Validate your `manifest.json` with [JSON Schema](https://github.com/kintone/js-sdk/tree/master/packages/plugin-manifest-validator)

# How to install

```console
$ npm install -g @kintone/plugin-packer
```

# Usage: CLI

```console
$ kintone-plugin-packer [OPTIONS] PLUGIN_DIR
```

## Options

- `--ppk PPK_FILE`: The path of input private key file. If omitted, it is generated automatically into `<Plugin ID>.ppk` in the same directory of `PLUGIN_DIR` or `--out` if specified.
- `--out PLUGIN_FILE`: The path of generated plugin file. The default is `plugin.zip` in the same directory of `PLUGIN_DIR`.
- `--watch`, `-w`: Watch PLUGIN_DIR for the changes.

## How to use with `npm run`

If your private key is `./private.ppk` and the plugin directory is `./plugin`, edit `package.json`:

```json
{
  "scripts": {
    "package": "kintone-plugin-packer --ppk private.ppk plugin"
  }
}
```

and then

```console
$ npm run package
```

# Usage: Node.js API

```js
const packer = require('@kintone/plugin-packer');
const fs = require('fs');

const buffer = createContentsZipBufferInYourSelf();
packer(buffer).then(output => {
  console.log(output.id);
  fs.writeFileSync('./private.ppk', output.privateKey);
  fs.writeFileSync('./plugin.zip', output.plugin);
});
```

## License

MIT License
