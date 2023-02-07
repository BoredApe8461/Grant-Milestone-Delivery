# Milestone Delivery :mailbox:

**The [invoice form :pencil:](https://docs.google.com/forms/d/e/1FAIpQLSfmNYaoCgrxyhzgoKQ0ynQvnNRoTmgApz9NrMp-hd8mhIiO0A/viewform) has been filled out correctly for this milestone and the delivery is according to the official [milestone delivery guidelines](https://github.com/w3f/Grants-Program/blob/master/docs/milestone-deliverables-guidelines.md).**  



* **Application Document:** [Societal Application](https://github.com/w3f/Grants-Program/blob/master/applications/societal_grant2.md) 
* **Milestone Number:** 1



## Deliverables


| Number | Deliverable | Link | Notes |
| ------------- | ------------- | ------------- |------------- |
| 0a. | License |[GitHub repo link](https://github.com/sctllabs/societal-grant-2-submission/blob/main/LICENSE)| Apache 2.0 license included. |
| 0b. | Documentation |[GitHub repo link](https://github.com/sctllabs/societal-grant-2-submission/blob/main/README.md) | Readme document contains instructions on how to run and deploy societal front-end. All unit test have been included in the submission and can be run using: `cargo test` . Link to test command in [docs](https://github.com/sctllabs/societal-grant-2-submission#unit-test) |
| 0c. | Testing Guide |[GitHub repo link](https://github.com/sctllabs/societal-grant-2-submission/blob/main/docs/AssetsTestingGuide.md)| Guide on how to test Assets Pallet Lockable/Reservable traits using Polkadot-JS front-end. |
| 0d. | Docker |[Docker Image](https://hub.docker.com/layers/societal/societal-node/vb4f81a4/images/sha256-69ba2805d6eb08d8bd5721afc4c82d2975a368efcde2634356ba6568a9111e9d?context=explore)| Dockerfile found at Societal's docker hub. The tag information is as follows: **docker pull societal/societal-node:vb4f81a4**. Please refer to the [Run in Docker](https://github.com/sctllabs/societal-grant-2-submission#run-in-docker) section of the README to run with the **vb4f81a4** tag specified. |
| 1. | Substrate Module: Reservable & Lockable Asset Pallet |[GitHub repo link](https://github.com/sctllabs/societal-grant-2-submission) | The custom substrate assets pallet in this repo from Milestone 1 will allow any user to use Lockable/Reservable traits similar to the native balances pallet hash. It is helpful when used for DAO governance where you need to reserve DAO token while proposing and lock tokens while voting.  |  
| 2. | Client Modules | [Polkadot-JS](https://polkadot.js.org/apps/#/explorer?rpc=ws://localhost:9944) | You can use Polkadot-JS to interact with the DAO factory pallets and follow the [Testing Article](https://github.com/sctllabs/societal-grant-2-submission/blob/main/docs/AssetsTestingGuide.md) on how to work with the custom traits of the Assets Pallet. A more detailed UI will be delievered with milestone 2.  |
