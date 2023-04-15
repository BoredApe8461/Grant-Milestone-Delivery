# Evaluation

- **Status:** Accepted
- **Application Document:** [Coong Wallet](https://github.com/w3f/Grants-Program/blob/master/applications/coong_wallet.md). 
- **Milestone:** 1
- **Kusama Identity:** Eexv1mKLiCidz2gGh6vfowtXgSSc7mvD4xEb2ji998W4DPs
- **Previously successfully merged evaluation:** N/A

| Number | Deliverable                | Accepted               | Link                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 | Evaluation Notes                                                                                                             |
|--------|----------------------------|------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------|
| 0a.    | License                    | <ul><li>[x] </li></ul> | [Apache 2.0](https://github.com/CoongCrafts/coong-wallet/blob/w3f-milestone-1/LICENSE)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Correct License                                                                                                              |
| 0b.    | Documentation              | <ul><li>[x] </li></ul> | - [README](https://github.com/CoongCrafts/coong-wallet/blob/w3f-milestone-1/README.md)<br/> - [Live Demo](https://app.coongwallet.io/)<br/>- [Example DApp](https://coong-demo-dapp.netlify.app/)<br/>- [Integration Instructions](https://github.com/CoongCrafts/coong-wallet/blob/w3f-milestone-1/README.md#integrate-coong-wallet-into-your-dapps)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                | Improved in the recent [commit](https://github.com/CoongCrafts/coong-wallet/commit/3a3c11843be640c5582ecfd66c8ad0fe442db869) |
| 0c.    | Tests / Testing Guide      | <ul><li>[x] </li></ul> | - [How to run tests](https://github.com/CoongCrafts/coong-wallet/tree/w3f-milestone-1#how-to-run-tests)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              | All test cases passed successfully                                                                                           |
| 0d.    | Docker                     | <ul><li>[x] </li></ul> | - [Dockerfile](https://github.com/CoongCrafts/coong-wallet/blob/w3f-milestone-1/Dockerfile)<br/>- [How to run app in docker](https://github.com/CoongCrafts/coong-wallet/blob/w3f-milestone-1/README.md#run-it-on-docker)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            | Docker image built and working as expected, great work!.                                                                     |
| 1.     | Wallet App / Core Features | <ul><li>[x] </li></ul> | - [Welcome Screen](https://github.com/CoongCrafts/coong-wallet/blob/w3f-milestone-1/packages/ui/src/components/pages/Welcome.tsx)<br/>- [Unlock Wallet](https://github.com/CoongCrafts/coong-wallet/blob/w3f-milestone-1/packages/ui/src/components/pages/UnlockWallet.tsx)<br/>- [Setup New Wallet](https://github.com/CoongCrafts/coong-wallet/tree/w3f-milestone-1/packages/ui/src/components/pages/NewWallet/index.tsx)<br/>- [Create account](https://github.com/CoongCrafts/coong-wallet/blob/w3f-milestone-1/packages/ui/src/components/shared/NewAccountButton.tsx)<br/>- [List Accounts](https://github.com/CoongCrafts/coong-wallet/blob/w3f-milestone-1/packages/ui/src/components/pages/Accounts/index.tsx)<br/>- [Request Wallet Access](https://github.com/CoongCrafts/coong-wallet/blob/w3f-milestone-1/packages/ui/src/components/pages/Request/RequestAccess/index.tsx)<br/>- [Approve Transaction](https://github.com/CoongCrafts/coong-wallet/blob/w3f-milestone-1/packages/ui/src/components/pages/Request/RequestTransactionApproval/index.tsx) | Features listed here are working fine.                                                                                       |
| 2.     | Coong SDK                  | <ul><li>[x] </li></ul> | - [Source Code](https://github.com/CoongCrafts/coong-wallet/tree/w3f-milestone-1/packages/sdk)<br/>- [@coong/sdk](https://www.npmjs.com/package/@coong/sdk)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | SDK implemented and the package published successfully to npm registry as mentioned in the application                       |


## General Notes

### Update 21st March 2023
The docker build are yarn test errors are resolved. I was able to build and run the docker image successfully. Inline documentation has been improved in the recent [commit](https://github.com/CoongCrafts/coong-wallet/commit/3a3c11843be640c5582ecfd66c8ad0fe442db869) too, and I hope the READMe and inline documentation would include more details in the upcoming milestones. Overall, it's a great submission and great work.
### 20th March 2023
Core features of the wallet, as mentioned in the contract, are working great. It just needs some inline documentation for the code (e.g, one can't understand the purpose of [these](https://github.com/CoongCrafts/coong-wallet/blob/w3f-milestone-1/packages/keyring/src/types.ts#L4) types without a proper documentation), the docker issues and `yarn test` errors should be resolved as well. 

Overall, it's a good submission, it just needs some minor improvements.
### Docker Error
`docker build -t coong-wallet .` command failed with the following error:
```console
[+] Building 3.0s (11/11) FINISHED                                                                                                                                                           
 => [internal] load build definition from Dockerfile                                                                                                                                    0.0s
 => => transferring dockerfile: 32B                                                                                                                                                     0.0s
 => [internal] load .dockerignore                                                                                                                                                       0.0s
 => => transferring context: 34B                                                                                                                                                        0.0s
 => [internal] load metadata for docker.io/library/node:18                                                                                                                              2.4s
 => [internal] load build context                                                                                                                                                       0.0s
 => => transferring context: 12.81kB                                                                                                                                                    0.0s
 => [1/7] FROM docker.io/library/node:18@sha256:8d9a875ee427897ef245302e31e2319385b092f1c3368b497e89790f240368f5                                                                        0.0s
 => CACHED [2/7] RUN yarn policies set-version 3.4.1                                                                                                                                    0.0s
 => CACHED [3/7] WORKDIR /app                                                                                                                                                           0.0s
 => CACHED [4/7] COPY package.json .                                                                                                                                                    0.0s
 => CACHED [5/7] COPY yarn.lock .                                                                                                                                                       0.0s
 => CACHED [6/7] COPY . .                                                                                                                                                               0.0s
 => ERROR [7/7] RUN yarn install                                                                                                                                                        0.5s
-----                                                                                                                                                                                      
  [7/7] RUN yarn install:                                                                                                                                                                   
#0 0.397 node:internal/modules/cjs/loader:1078                                                                                                                                               
#0 0.397   throw err;                                                                                                                                                                        
#0 0.397   ^                                                                                                                                                                                 
#0 0.397                                                                                                                                                                                     
#0 0.397 Error: Cannot find module '/app/.yarn/releases/yarn-3.4.1.cjs'
#0 0.397     at Module._resolveFilename (node:internal/modules/cjs/loader:1075:15)
#0 0.397     at Module._load (node:internal/modules/cjs/loader:920:27)
#0 0.397     at Function.executeUserEntryPoint [as runMain] (node:internal/modules/run_main:81:12)
#0 0.397     at node:internal/main/run_main_module:23:47 {
#0 0.397   code: 'MODULE_NOT_FOUND',
#0 0.397   requireStack: []
#0 0.397 }
#0 0.397 
#0 0.397 Node.js v18.15.0
------
ERROR: failed to solve: executor failed running [/bin/sh -c yarn install]: exit code: 1
```

### Yarn Tests error
All the tests passed successfully, but I got this error on my terminal:
```
Error: Uncaught [Error: InvalidMessageFormat]
    at reportException (coong-wallet/node_modules/jsdom/lib/jsdom/living/helpers/runtime-script-errors.js:66:24)
    at innerInvokeEventListeners (coong-wallet/node_modules/jsdom/lib/jsdom/living/events/EventTarget-impl.js:353:9)
    at invokeEventListeners (coong-wallet/node_modules/jsdom/lib/jsdom/living/events/EventTarget-impl.js:286:3)
    at HTMLUnknownElementImpl._dispatch (coong-wallet/node_modules/jsdom/lib/jsdom/living/events/EventTarget-impl.js:233:9)
    at HTMLUnknownElementImpl.dispatchEvent (coong-wallet/node_modules/jsdom/lib/jsdom/living/events/EventTarget-impl.js:104:17)
    at HTMLUnknownElement.dispatchEvent (coong-wallet/node_modules/jsdom/lib/jsdom/living/generated/EventTarget.js:241:34)
    at Object.invokeGuardedCallbackDev (coong-wallet/node_modules/react-dom/cjs/react-dom.development.js:4213:16)
    at invokeGuardedCallback (coong-wallet/node_modules/react-dom/cjs/react-dom.development.js:4277:31)
    at reportUncaughtErrorInDEV (coong-wallet/node_modules/react-dom/cjs/react-dom.development.js:22838:5)
    at captureCommitPhaseError (coong-wallet/node_modules/react-dom/cjs/react-dom.development.js:27126:5) CoongError: InvalidMessageFormat
    at coong-wallet/packages/ui/src/components/pages/Request/index.tsx:39:13
    at commitHookEffectListMount (coong-wallet/node_modules/react-dom/cjs/react-dom.development.js:23150:26)
    at commitPassiveMountOnFiber (coong-wallet/node_modules/react-dom/cjs/react-dom.development.js:24931:11)
    at commitPassiveMountEffects_complete (coong-wallet/node_modules/react-dom/cjs/react-dom.development.js:24891:9)
    at commitPassiveMountEffects_begin (coong-wallet/node_modules/react-dom/cjs/react-dom.development.js:24878:7)
    at commitPassiveMountEffects (coong-wallet/node_modules/react-dom/cjs/react-dom.development.js:24866:3)
    at flushPassiveEffectsImpl (coong-wallet/node_modules/react-dom/cjs/react-dom.development.js:27039:3)
    at flushPassiveEffects (coong-wallet/node_modules/react-dom/cjs/react-dom.development.js:26984:14)
    at coong-wallet/node_modules/react-dom/cjs/react-dom.development.js:26769:9
    at flushActQueue (coong-wallet/node_modules/react/cjs/react.development.js:2667:24) {
  code: 'InvalidMessageFormat'
}
```

