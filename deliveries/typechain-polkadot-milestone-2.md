# Milestone Delivery :mailbox:


**The [invoice form :pencil:](https://docs.google.com/forms/d/e/1FAIpQLSfmNYaoCgrxyhzgoKQ0ynQvnNRoTmgApz9NrMp-hd8mhIiO0A/viewform) has been filled out correctly for this milestone and the delivery is according to the official [milestone delivery guidelines](https://github.com/w3f/Grants-Program/blob/master/docs/milestone-deliverables-guidelines.md).**

* **Application Document:** https://github.com/w3f/Grants-Program/blob/master/applications/typechain-polkadot-follow-up.md
* **Milestone Number:** 2

**Context** (optional)
> Please provide a short paragraph or two connecting the deliverables in this milestone and describing their purpose.

**Deliverables**
> Please provide a list of all deliverables of the milestone extracted from the initial application and a link to the deliverable itself. Ideally all links inside the below table should include a commit hash, which will be used for testing. If you don't provide a commit hash, we will work off the default branch of your repository. Thus, if you plan on continuing work after delivery, we suggest you create a separate branch for either the delivery or your continuing work.
>
> If there is anything particular about any of the deliverables we or a future reader should know, use the respective `Notes` column.

| Number | Deliverable                                                                          | Link                                                                      | Notes                                                                                                           |
|-------|--------------------------------------------------------------------------------------|---------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|
| 0a    | License                                                                              | https://github.com/727-Ventures/typechain-polkadot/blob/master/LICENSE | MIT                                                                                                             |
 | 0b    | Documentation | https://github.com/727-Ventures/typechain-polkadot/tree/master/docs    | We added docs for functions, and also auto-generated docs                                                       |
| 1     | Investigation & Refactoring | https://github.com/727-Ventures/typechain-polkadot                     | Due to the lack of documentation we had to investigate how polkadot.js works under the hood directly in the source code and fixed bugs with new versions of substrate and polkadot.js, such as problems with gasLimits. We had some problems with new versions of substrate-contracts-node, before we used default gasLimit as -1 and now we are using just big number, feel free to check out our commit https://github.com/727-Ventures/typechain-polkadot/commit/710896c7b9f2677a97f7b84cbf035c5c8fb1996d in file packages/typechain-polkadot/src/output-generators/raw/_sdk/query.ts. We have created preprocessAbi function and added _ before each type’ display name, it was done because of polkadot-js can optimize usage of known types such as Balance, and change it interface that can break typechain-polkadot-parser. We figured out with ink! 4 update abi changed a little bit, and in some places we used raw abi (mainly in preprocessABI function) so we created __getV3 function that gets everything we need no matter which ink version we are using. You can check that here https://github.com/727-Ventures/typechain-polkadot/blob/master/packages/typechain-polkadot/src/output-generators/_utils.ts#L88. All types are covered, thanks to parser-module, and we've refactored our structure to monorepo            |
| 2     | Parser & generators modules | https://github.com/727-Ventures/typechain-polkadot/tree/master/packages | We separated parser and typechain into two separate packages, and added Handlebars templates for generating code |
| 3     | Contract deployment | https://github.com/727-Ventures/typechain-polkadot/blob/master/packages/typechain-polkadot/src/templates/constructors.hbs. Guide: https://github.com/727-Ventures/typechain-polkadot/blob/master/packages/typechain-polkadot/README.md#constructors | We added a constructors namespace for contract deployment                                                       |
| 4a    | Contract classes extension | https://github.com/727-Ventures/typechain-polkadot/blob/master/packages/typechain-polkadot/src/templates/contract.hbs | We added a new methods to Contract class for contract interaction                       | 
| 4b    | Methods' names | https://github.com/727-Ventures/typechain-polkadot/blob/master/packages/typechain-polkadot/src/output-generators/_utils.ts | Formatting of methods names is done in preprocessAbi function |
| 5 | Testing | https://github.com/727-Ventures/typechain-polkadot/tree/master/packages/typechain-polkadot/tests | PSP22 is covered with typechain-polkadot. Feel free to checkout out our guide how to run tests: https://github.com/727-Ventures/typechain-polkadot/blob/master/packages/typechain-polkadot/tests/README.md
| 6 | Article | https://medium.com/727-ventures/typechain-polkadot-overview-7c184067523f | An article about typechain-polkadot | 
| 7 | Branding | https://medium.com/727-ventures/typechain-polkadot-overview-7c184067523f | We have created logotype for typechain-polkadot |
 
