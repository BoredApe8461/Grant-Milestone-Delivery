# Milestone Delivery :mailbox:

> ⚡ Only the GitHub account that submitted the application is allowed to submit milestones. 
> 
> Don't remove any of the mandatory parts presented in bold letters or as headlines! Lines starting with `>`, such as this one, can be removed.

**The [invoice form :pencil:](https://docs.google.com/forms/d/e/1FAIpQLSfmNYaoCgrxyhzgoKQ0ynQvnNRoTmgApz9NrMp-hd8mhIiO0A/viewform) has been filled out correctly for this milestone and the delivery is according to the official [milestone delivery guidelines](https://github.com/w3f/Grants-Program/blob/master/docs/milestone-deliverables-guidelines.md).**  

* **Application Document:** https://github.com/w3f/Grants-Program/blob/master/applications/pallet_supersig.md
* **Milestone Number:** 2

**Context** 

Supersig is like multisig but with superpowers. This means that you have some added features such as :

- you can add and remove members from the supersig.
- you get simpleMajority, instead of fixed thresholds. 
- you get a master superuser feature. A master user always has 50% of the voting power. This means that if a master user is involved in a transaction, only one other person needs to sign in order to approve the transaction for execution. (More than one person can be a master user). 

Supersig is now part of Kabocha parachain's mainnet on Kusama. 

Milestone 1 was about building pallet_supersig's first version. The pallet now allows you to do the abovementioned core functions. 

Milestone 2 is about adding user interface within the "apps" frontend environment. This will be at home in https://apps.decentration.org. 

**Deliverables**
> Please provide a list of all deliverables of the milestone extracted from the initial application and a link to the deliverable itself. Ideally all links inside the below table should include a commit hash, which will be used for testing. If you don't provide a commit hash, we will work off the default branch of your repository. Thus, if you plan on continuing work after delivery, we suggest you create a separate branch for either the delivery or your continuing work. 
> 
> If there is anything particular about any of the deliverables we or a future reader should know, use the respective `Notes` column.

| Number | Deliverable | Link | Notes |
| -----: | ----------- | ------------- | ---------- | 
| 0a. | License | Apache 2.0  |  | |
| 0b. | Documentation | https://decentration.medium.com/setup-for-testing-supersig-ui-m2-fac2f7ab20a3, https://wiki.kabocha.network/docs/Supersig/introduction | 2 links |
| 0c. | Testing Guide | https://github.com/kabocha-network/pallet_supersig/tree/polkadot-v0.9.28/src/tests | cargo test `INSERT FILENAME` |
| 0d. | Docker |  https://github.com/decentration/substrate-supersig-template/tree/v0.9.28-new | |
| 0e. | Article  | https://decentration.medium.com/supersig-like-multisig-but-with-superpowers-86b9ce0412f6,   https://www.loom.com/share/dbcaa6319b1a4644aacb709aa0e38783 | Article and video for reviewers |
| 1. | Substrate module: pallet_supersig |  pallet_supersig https://github.com/kabocha-network/pallet_supersig/blob/polkadot-v0.9.28/src/lib.rs | |
| 2. | Substrate-supersig template Chain | node-template containing pallet supersig and rpc functions https://github.com/decentration/substrate-supersig-template | |
| 3. | Polkadot JS Apps UI Fork | https://github.com/decentration/apps/tree/page-supersig-m2-new  | use branch `page-supersig-m2-new` be sure to follow this guide with simple steps to install everything https://decentration.medium.com/setup-for-testing-supersig-ui-m2-fac2f7ab20a3 | |

**Additional Information**
> Any further comments on the milestone that you would like to share with us.
