
# Yatima Milestone Delivery :mailbox:

> ⚡ Only the GitHub account, which is responsible for the pull request of the accepted application is allowed to submit milestones. 
> 
> Don't remove any of the mandatory parts presented in bold letters or as headlines! Lines starting with `>`, such as this one, can be removed.

**The [invoice form :pencil:](https://docs.google.com/forms/d/e/1FAIpQLSfmNYaoCgrxyhzgoKQ0ynQvnNRoTmgApz9NrMp-hd8mhIiO0A/viewform) has been filled out correctly for this milestone and the delivery is according to the official [milestone delivery guidelines](https://github.com/w3f/General-Grants-Program/blob/master/grants/milestone-deliverables-guidelines.md).**  

* **Application Document:** [Yatima Open Grant Proposal](https://github.com/yatima-inc/Open-Grants-Program/blob/e122eb754e9c4c228dea6721e6822fef4953cb30/applications/yatima.md) 
* **Milestone Number:** 1

> Please provide a list of all deliverables of the milestone extracted from the initial application and a link to the deliverable itself. Ideally all links inside the below table should include a commit hash, which will be used for testing. If you don't provide a commit hash, we will work off the default branch of your repository. Thus, if you plan on continuing work after delivery, we suggest you create a separate branch for either the delivery or your continuing work. 
> 
> If there is anything particular about any of the deliverables we or a future reader should know, use the respective `Notes` column.

| Number        | Deliverable                      | Link                                                                   | Notes                                                                                                                                                                                                   |
| ------------- | -------------                    | -------------                                                          | -------------                                                                                                                                                                                           |
| 0a.           | License                          | [LICENSE](https://github.com/yatima-inc/sp-ipld/blob/main/LICENSE)     | MIT                                                                                                                                                                                                     |
| 0b.           | Documentation                    | [README](https://github.com/yatima-inc/sp-ipld/blob/main/README.md)    | Added inline documentation and wrote a [tutorial](https://github.com/yatima-inc/sp-ipld/blob/main/substrate-tutorial.md) on `sp-ipld` usage within Substrate                                                                                                                     |
| 0c.           | Testing Guide                    | [README](https://github.com/yatima-inc/sp-ipld/blob/main/README.md)    | Extended existing unit tests with more coverage, and added quickcheck property tests and integration tests with `go-ipfs` for ensuring CID compatibility                                                |
| 0d.           | Nix                              | [flake.nix](https://github.com/yatima-inc/sp-ipld/blob/main/flake.nix) | Created a `.nix` expression to immutably build `sp-ipld` and each Substrate module                                                                                                                      |
| 1a.           | Substrate module: `sp-ipld`      | [sp-ipld](https://github.com/yatima-inc/sp-ipld)                       | Created a Substrate module based on `ipfs-rust/libipld` that allows for serializing and deserializing IPLD objects via the `dag-cbor` codec and computing IPFS CIDs which are compatible with `go-ipfs` |
| 1b.           | `dag-json` feature               | [sp-ipld/src](https://github.com/yatima-inc/sp-ipld/tree/main/src)     | Implemented the `dag-json` codec for the `sp_ipld` module as a parse/print frontend to `dag-cbor`, as well as a textual JSON format                                                                     |
| 1c.           | Substrate module: `sp-cid`       | [sp-cid](https://github.com/yatima-inc/sp-cid)                         | Implemented a documented `no_std` version of the `ipfs-rust/libipld` dependency `multiformats/rust-cid`                                                                                                 |
| 1d.           | Substrate module: `sp-multihash` | [sp-multihash](https://github.com/yatima-inc/sp-multihash)             | Implemented a documented `no_std` version of the `ipfs-rust/libipld` dependency `multiformats/rust-multihash`                                                                                           |
| 1e.           | Substrate module: `bytecursor`   | [bytecursor](https://github.com/yatima-inc/bytecursor)                 | Implemented a documented `no_std` drop-in replacement library for the `std::io::Read` and `std::io::Write` based serialization/deserialization functions used by `ipfs-rust/libipld`                    |
