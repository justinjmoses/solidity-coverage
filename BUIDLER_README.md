[![Gitter chat](https://badges.gitter.im/sc-forks/solidity-coverage.svg)][18]
![npm (tag)](https://img.shields.io/npm/v/solidity-coverage/beta)
[![CircleCI](https://circleci.com/gh/sc-forks/solidity-coverage.svg?style=svg)][20]
[![codecov](https://codecov.io/gh/sc-forks/solidity-coverage/branch/beta/graph/badge.svg)][21]
[![buidler](https://buidler.dev/buidler-plugin-badge.svg?1)][26]

# solidity-coverage

Solidity code coverage plugin for [buidler](http://getbuidler.com).

## What

![coverage example][22]

+ For more details about how it works and potential limitations, see [the accompanying article][16].
+ `solidity-coverage` is also [JoinColony/solcover][17]


## Installation

```bash
$ npm install --save-dev solidity-coverage@beta
```

And add the following to your `buidler.config.js`:

```js
usePlugin("solidity-coverage");
```

## Tasks

This plugin implements a `coverage` task

```bash
npx buidler coverage [options]
```

| Option <img width=200/> | Example <img width=750/>| Description <img width=1000/> |
|--------------|------------------------------------|--------------------------------|
| testfiles  | `--testfiles test/file.js` | JS test file(s) to run.|
| solcoverjs | `--solcoverjs ./../.solcover.js` | Relative path from working directory to config. Useful for monorepo packages that share settings. (Path must be "./" prefixed) |
| network    | `--network development` | Use network settings defined in the Buidler config |


## Configuration

Options can be specified in a `.solcover.js` config file located in the root directory of your project.

**Project Examples:**

+ Simple: [buidler-metacoin][29]
+ More complex: [MolochDao/moloch][30]

**Config Example:**
```javascript
module.exports = {
  skipFiles: ['Routers/EtherRouter.sol']
};
```

| Option <img width=200/>| Type <img width=200/> | Default <img width=1300/> | Description <img width=800/> |
| ------ | ---- | ------- | ----------- |
| silent | *Boolean* | false | Suppress logging output |
| client | *Object* | `require("ganache-core")` | Useful if you need a specific ganache version. |
| providerOptions | *Object* | `{ }` | [ganache-core options][1]  |
| skipFiles | *Array* | `['Migrations.sol']` | Array of contracts or folders (with paths expressed relative to the `contracts` directory) that should be skipped when doing instrumentation. |
| istanbulFolder | *String* | `./coverage` |  Folder location for Istanbul coverage reports. |
| istanbulReporter | *Array* | `['html', 'lcov', 'text', 'json']` | [Istanbul coverage reporters][2]  |
| mocha | *Object* | `{ }` | [Mocha options][3] to merge into existing mocha config. `grep` and `invert` are useful for skipping certain tests under coverage using tags in the test descriptions.|
| onServerReady[<sup>*</sup>][14] | *Function* |   | Hook run *after* server is launched, *before* the tests execute. Useful if you need to use the Oraclize bridge or have setup scripts which rely on the server's availability. [More...][23] |
| onCompileComplete[<sup>*</sup>][14] | *Function* |  | Hook run *after* compilation completes, *before* tests are run. Useful if you have secondary compilation steps or need to modify built artifacts. [More...][23]|
| onTestsComplete[<sup>*</sup>][14] | *Function* |  | Hook run *after* the tests complete, *before* Istanbul reports are generated. [More...][23]|
| onIstanbulComplete[<sup>*</sup>][14] | *Function* |  | Hook run *after* the Istanbul reports are generated, *before* the ganache server is shut down. Useful if you need to clean resources up. [More...][23]|

[<sup>*</sup> Advanced use][14]

## Usage

+ Coverage runs tests a little more slowly.
+ Coverage launches its own in-process ganache server.
+ You can set [ganache options][1] using the `providerOptions` key in your `.solcover.js` [config][15].
+ Coverage [distorts gas consumption][13]. Tests that check exact gas consumption should be [skipped][24].
+ :warning:  Contracts are compiled **without optimization**. Please report unexpected compilation faults to [issue 417][25]

## Documentation

More documentation, including FAQ and information about solidity-coverage's API [is available here][28].


[1]: https://github.com/trufflesuite/ganache-core#options
[2]: https://istanbul.js.org/docs/advanced/alternative-reporters/
[3]: https://mochajs.org/api/mocha
[4]: https://github.com/sc-forks/solidity-coverage/blob/beta/docs/faq.md#running-out-of-gas
[5]: https://github.com/sc-forks/solidity-coverage/blob/beta/docs/faq.md#running-out-of-memory
[6]: https://github.com/sc-forks/solidity-coverage/blob/beta/docs/faq.md#running-out-of-time
[7]: https://github.com/sc-forks/solidity-coverage/blob/beta/docs/faq.md#continuous-integration
[8]: https://github.com/sc-forks/solidity-coverage/blob/beta/docs/faq.md#notes-on-branch-coverage
[9]: https://sc-forks.github.io/metacoin/
[10]: https://coveralls.io/github/OpenZeppelin/openzeppelin-solidity?branch=master
[11]: https://github.com/sc-forks/solidity-coverage/tree/beta/test/units
[12]: https://github.com/sc-forks/solidity-coverage/issues
[13]: https://github.com/sc-forks/solidity-coverage/blob/beta/docs/faq.md#notes-on-gas-distortion
[14]: https://github.com/sc-forks/solidity-coverage/blob/beta/docs/advanced.md
[15]: #config-options
[16]: https://blog.colony.io/code-coverage-for-solidity-eecfa88668c2
[17]: https://github.com/JoinColony/solcover
[18]: https://gitter.im/sc-forks/solidity-coverage?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge
[19]: https://badge.fury.io/js/solidity-coverage
[20]: https://circleci.com/gh/sc-forks/solidity-coverage
[21]: https://codecov.io/gh/sc-forks/solidity-coverage
[22]: https://cdn-images-1.medium.com/max/800/1*uum8t-31bUaa6dTRVVhj6w.png
[23]: https://github.com/sc-forks/solidity-coverage/blob/beta/docs/advanced.md#workflow-hooks
[24]: https://github.com/sc-forks/solidity-coverage/blob/beta/docs/advanced.md#skipping-tests
[25]: https://github.com/sc-forks/solidity-coverage/issues/417
[26]: https://buidler.dev/
[27]: https://www.trufflesuite.com/docs
[28]: https://github.com/sc-forks/solidity-coverage/blob/beta/README.md
[29]: https://github.com/sc-forks/buidler-e2e/tree/coverage
[30]: https://github.com/sc-forks/moloch

