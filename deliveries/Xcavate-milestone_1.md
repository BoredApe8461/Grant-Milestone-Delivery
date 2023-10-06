# Milestone Delivery :mailbox:

> ⚡ Only the GitHub account that submitted the application is allowed to submit milestones. 

**The [invoice form :pencil:](https://docs.google.com/forms/d/e/1FAIpQLSfmNYaoCgrxyhzgoKQ0ynQvnNRoTmgApz9NrMp-hd8mhIiO0A/viewform) has been filled out correctly for this milestone and the delivery is according to the official [milestone delivery guidelines](https://github.com/w3f/Grants-Program/blob/master/docs/Support%20Docs/milestone-deliverables-guidelines.md).**  

* **Application Document:** https://github.com/w3f/Grants-Program/blob/master/applications/Xcavate.md
* **Milestone Number:** 1

**Context** (optional)
> We have built a fully functioning substrate based node + react.js Frontend + node.js backend dApp for user interaction

**Deliverables**
> Please see deliverables below; including some testing documentation & a video to guide you through the specific lending protocol and smart contract deliverables.


| Number | Deliverable | Link | Notes |
| ------------- | ------------- | ------------- |------------- |
| 0a.  | License | Apache 2.0 | |
| 0b.  | Documentation | [https://xcavate.gitbook.io/xcavate-documentation/] | please see this high level process flow to give you a better understanding of the overall interactions |
| 0c. | Testing video | [https://youtu.be/LxOwFm4XDrw] | A comprehensive video walking through all aspects of the loan process & functionality |
| 0d. | Testing Guide | [https://github.com/XcavateBlockchain/MVP_Lending_Pool/blob/MVP_Lending_Protocol/README.m] [https://github.com/XcavateBlockchain/lending_protocol_contracts/blob/main/README.md] | Documentation to guide the tester through loan process & functionality |
| 1. | Xcavate Node Repo | [https://github.com/XcavateBlockchain/MVP_Lending_Pool] | This is a fully functioning substrate node | 
| 2.  | Xcavate Loan App Repo | [https://github.com/XcavateBlockchain/lending_protocol_contracts] | Ink! based contracts that interact with the contracts pallet | 
| 3.  | Loan management pallet | [https://github.com/XcavateBlockchain/MVP_Lending_Pool/tree/MVP_Lending_Protocol/pallets/community-loan-pool] | Actually called Community Loan Pallet - A percentage of all XCAV tokens will be deposited in an account, once minted, to facilitate all approved real estate developer loans  |
| 4.  | Community Loan Staking pallet | [https://github.com/XcavateBlockchain/MVP_Lending_Pool/tree/MVP_Lending_Protocol/pallets/xcavate-staking] | Community Loan Staking - This is its basic format... additional work is needed to make production ready  | 
| 5.  | Verification pallet | [https://github.com/XcavateBlockchain/kilt-credentials] | Not a pallet - It leverages the KILT protocol - going forward this will be a DID pallet that communicates with KILT via XCM  | 
| 6.  | DAO | [https://github.com/XcavateBlockchain/MVP_Lending_Pool/blob/MVP_Lending_Protocol/node/Cargo.toml] | Our chain uses the SUDO pallet... this will continue until it has matured enough for the full community governance structure to be implemented  | 
| 7a.  | Decentralized Developer Loan dApp / Front End Repo part 1 | [https://github.com/XcavateBlockchain/MVP_Frontend] | React.js Frontend | 
| 7b.  | Decentralized Developer Loan dApp / Front End Repo part 2 | [https://github.com/XcavateBlockchain/MVP_Backend] | node.js Backend | 
| 7c.  | Decentralized Developer Loan dApp / Front End Repo part 3 | [https://github.com/XcavateBlockchain/MVP_Admin] | Backend admin - to enable credential attestation | 
| 8.  | Docker | Despite our best efforts we could not get the substrate node template to save as a docker image - however it works perfectly well using VS Code | 
| 9.  | Tutorial | [https://xcavate.gitbook.io/xcavate-documentation/tutorial-and-testing-guide] | Real Estate Developer Loan Instructions & How the Xcavate network functions | 
| 10.  | Article | [https://xcavate.io/revolutionizing-real-estate-development-financing-with-nft-backed-loans/] | This blog article explores the revolutionalising aspect of utilising NFT backed Real Estate Development Loans  | 



**Additional Information**
> While we have made great progress with this project + we are confident we can deliver this as a live project within the Dotsama ecosystem. There is quite a bit more work to be done and as such would require additional funding if available.
