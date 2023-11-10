# LiveConnect

[![BrowserStack Status](https://automate.browserstack.com/badge.svg?badge_key=YzloV1dIQUNFOHFkOXlJRUxLNXZxSEFvTVVOSHVIVGFHS05tdnNicTRpTT0tLVVVOUpGWUE2SEJNTlZpT2xnSVBjYmc9PQ==--cfc32e5172c470536344a9c6b751a20019aab049)](https://automate.browserstack.com/public-build/YzloV1dIQUNFOHFkOXlJRUxLNXZxSEFvTVVOSHVIVGFHS05tdnNicTRpTT0tLVVVOUpGWUE2SEJNTlZpT2xnSVBjYmc9PQ==--cfc32e5172c470536344a9c6b751a20019aab049)
[![CircleCI](https://circleci.com/gh/LiveIntent/live-connect/tree/master.svg?style=svg)](https://circleci.com/gh/LiveIntent/live-connect/tree/master)
[![codecov](https://codecov.io/gh/LiveIntent/live-connect/branch/master/graph/badge.svg?token=P5sRpM4U6k)](https://codecov.io/gh/LiveIntent/live-connect)
[![CodeQL](https://github.com/LiveIntent/live-connect/actions/workflows/codeql.yml/badge.svg?branch=master&event=push)](https://github.com/LiveIntent/live-connect/actions/workflows/github-code-scanning/codeql)
[![dependencies Status](https://img.shields.io/librariesio/release/npm/live-connect)](https://github.com/LiveIntent/live-connect/tree/master)

## Main concepts
The LiveConnect module offers a convenient solution for generating and collecting first-party identifiers based on your preferences, and sending this information to a designated endpoint. With LiveConnect, you gain a straightforward interface that facilitates the collection of identifiers from web pages, as well as capturing user interactions alongside these identifiers.
If you're interested in reviewing the type of data being sent, please check [what is being sent](#what-is-being-sent) section of this documentation.

## Quick start
To quickly get started with the LiveConnect module, perform the following steps via the command line interface.

- Dependency installation: Begin by installing the dependencies using npm. Run the following command: `npm install`.
- Code formatting: Ensure your code adheres to the provided ESLint file for consistent formatting. Use the command `npm run fix-js` to automatically format your code.
- Unit testing: Validate the functionality of your code by running the unit tests. Execute the command `npm run test:unit` to initiate the tests.
- Integration testing: Verify the integration of LiveConnect by running the integration tests against a dockerized Chrome browser. Use the command `npm run test:it:docker:chrome` to perform these tests.
- Cross-browser testing: For a comprehensive evaluation, conduct full integration tests on multiple browsers. Please ensure you have valid Browserstack credentials configured. Run the command `npm run test:it:browserstack` to execute the tests across various browsers.

## Contribute
We welcome ideas, fixes, and improvements from the community. Discover how you can contribute by visiting our [contribution guidelines](./CONTRIBUTING.md).

## Testing
### Running Unit tests
Unit tests are written using [Mocha](http://mochajs.org/) and [Chai](http://chaijs.com/).
Check [Quick start](#quick-start) how to run them.

### Running Browserstack tests
Tests sets the cookies on eTLD+1 domain. For that, execute the following command:
```echo "127.0.0.1 bln.test.liveintent.com" | sudo tee -a /etc/hosts && echo "127.0.0.1 test.liveintent.com" | sudo tee -a /etc/hosts && echo "127.0.0.1 me.idex.com" | sudo tee -a /etc/hosts && echo "127.0.0.1 schmoogle.com" | sudo tee -a /etc/hosts && echo "127.0.0.1 framed.test.liveintent.com" | sudo tee -a /etc/hosts && echo "127.0.0.1 double-framed.test.liveintent.com" | sudo tee -a /etc/hosts && echo "127.0.0.1 baked.liveintent.com" | sudo tee -a /etc/hosts```

Add Browserstack keys to your env, where the setup would be as follows:
```
user: process.env.BS_USER,
key: process.env.BS_KEY,
```
or, to run Browserstack tests locally, run:
```BS_USER=${User} BS_KEY=${Key} npm run test:it:browserstack```

The browsers used in these tests are defined in `test-config/wdio.browserstack.conf.js` and should correlate to the transpiled code for supported browsers, listed in `.browserslistrc`.
___

## Initialization
The initialisation part should be straight forward, considering the snippet:
```javascript
import { LiveConnect } from 'live-connect-js'
const lc = LiveConnect(configOptions)
```

The object returned after initialisation (`lc` in the snippet above) is exposing the following functions:
- `push` accepts a custom event one would like to keep track of.
- `fire` just fires a pixel, and can be considered as a simple page view.
- `peopleVerifiedId` returns the most likely first party cookie that can be used for identity resolution.
- `ready` flag, saying that the LC was loaded and ready, can be used when including LiveConnect as a global var on the window object.
- `resolve` function accepts a success callback, an error callback and an additional object with key value pairs. Of course, errors during resolution will be emitted on the EventBus and sent to the collector. The third parameter is `additionalParameters` which is an object, and will be attached to the IdentityResolution request, split into key-value pairs. The purpose of this object is to include key-value pairs in the request, e.g. for identifiers that cannot be found in the cookie jar, or in LocalStorage, or simply there's a requirement for a certain identifier to be represented under a specific key which doesn't match its name in the cookie jar, or LocalStorage key.
- `resolutionCallUrl` function returns the URL to be called in order to receive the resolution to a stable identifier.

## linda Ikeji Blog
[Lagos State Government News](https://www.lindaikejisblog.com/2023/11/lagos-state-government-cancels-50-discount-on-public-transport-2.html) 

`hello`

- hi

~~This is nigeria.~~

X<sup>2</sup>

H<sub>2</sub>0

<mark>liveconnect</mark>

Its a great day! ![Alt text](./image.png)

```
the file is updated 

update code only

merge text with code```

