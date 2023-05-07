# Evaluation

- **Status:** Accepted
- **Application Document:** https://github.com/w3f/Grants-Program/blob/master/applications/psc.md
- **Milestone:** 1
- **Kusama Identity:** [HC8pZ53SejB9YALHn2qXea6XMFFNgxpdXhVvtF7uU5dTSqu](https://kusama.subscan.io/account/HC8pZ53SejB9YALHn2qXea6XMFFNgxpdXhVvtF7uU5dTSqu)
- **Previously successfully merged evaluation:** All by 0xCaso

| Number | Deliverable | Accepted | Link | Evaluation Notes |
| ------ | ----------- | -------- | ---- |----------------- |
| 0a. | License | <ul><li>[x] </li></ul> | [`LICENSE`](https://github.com/OmniBTC/PSC/blob/a143c2da535d0969f6a0a5e682b24f9eb43c0873/LICENSE) |  | 
| 0b. | Documentation | <ul><li>[x] </li></ul> | [`README.md`](https://github.com/OmniBTC/PSC/blob/a143c2da535d0969f6a0a5e682b24f9eb43c0873/README.md) |  |
| 0c. | Testing and Testing Guide | <ul><li>[x] </li></ul> | [`/docs/test_guide.md`](https://github.com/OmniBTC/PSC/blob/a143c2da535d0969f6a0a5e682b24f9eb43c0873/docs/test_guide.md) | See **General Notes** |
| 0d. | Docker | <ul><li>[x] </li></ul> | [`/zombienet/psc-small-network.toml`](https://github.com/OmniBTC/PSC/blob/a143c2da535d0969f6a0a5e682b24f9eb43c0873/zombienet/psc-small-network.toml) | See **General Notes** |
| 0e. | Article | <ul><li>[x] </li></ul> | [`/docs/substrate_and_evm_address_on_psc.md`](https://github.com/OmniBTC/PSC/blob/a143c2da535d0969f6a0a5e682b24f9eb43c0873/docs/substrate_and_evm_address_on_psc.md) |  |
| 1. | Substrate module: pallet-assets-bridge | <ul><li>[x] </li></ul> | [`/pallets/assets-bridge`](https://github.com/OmniBTC/PSC/tree/a143c2da535d0969f6a0a5e682b24f9eb43c0873/pallets/assets-bridge) |  |
| 2. | Polkadot Smart Chain | <ul><li>[x] </li></ul> | [PSC repo](https://github.com/OmniBTC/PSC/tree/a143c2da535d0969f6a0a5e682b24f9eb43c0873) |  |
| 3. | Smart contracts: AssetsBridgeErc20 | <ul><li>[x] </li></ul> | [`/contracts`](https://github.com/OmniBTC/PSC/blob/a143c2da535d0969f6a0a5e682b24f9eb43c0873/contracts) |  |

<br/>

## General Notes v2 - Feb 20, 2023
- The team improved and fixed the testing guide, and now it's even more clear and easy to follow;
- The `remix.sh` script has been added;
- The other comments have been discussed in the PR discussion from [here](https://github.com/w3f/Grant-Milestone-Delivery/pull/745#issuecomment-1434160305).

<br/>

## General Notes v1 - Feb 16, 2023
I managed to follow the testing guide, which explains how to setup the local environment with both the relay chain and the parachain.
It's not been straightforward (but I think it's because that I've used a Macbook to test).

I report the following notes:
1. Could you please add tests for the Solidity contracts?
2. To make the command 
  
    ```bash
    zombienet-linux-x64 spawn --provider native ./psc-small-network.toml
    ```
    work (actually I didn't use `zombienet-linux-x64`), I edited `psc-small-network.toml` changing the `default_command` for the relay chain. and the `command` for the parachain (putting the full path to the binary). This because zombienet calls `bash -c`, and putting `polkadot` and `psc` in the path didn't work (I also tried to edit the `.bashrc` file, but it didn't work either). Maybe this problem is just related to the MacOS setup, but I think it's worth mentioning it;
3. In [this](https://github.com/OmniBTC/PSC/blob/da10743ae93948b54c92e6779496bce3c4120a88/docs/test_guide.md#24-transfer-dot-from-relaychain-to-parachain-by-dmp) part of the guide, the address is wrong (and are the decimamals the same [here](https://github.com/OmniBTC/PSC/blob/da10743ae93948b54c92e6779496bce3c4120a88/docs/test_guide.md#24-transfer-dot-from-relaychain-to-parachain-by-dmp) and [here](https://github.com/OmniBTC/PSC/blob/da10743ae93948b54c92e6779496bce3c4120a88/docs/test_guide.md#25-transfer-dot-from-parachain-to-relaychain-by-ump)?)
4. The `remix.sh` script mentioned [here](https://github.com/OmniBTC/PSC/blob/da10743ae93948b54c92e6779496bce3c4120a88/docs/test_guide.md#421-connect-remix) is missing (I managed to use remix in any case, but I wanted to note it);
5. With the function [`register`](https://github.com/OmniBTC/PSC/blob/da10743ae93948b54c92e6779496bce3c4120a88/docs/test_guide.md#43-bind-wasm-reserved0-and-erc20-reserved0) I can bind whatever address, also a user address. Is it possible to make a check / did you think about it?
6. If I try the setup with podman (so using Docker), I incur in the following error:
  
    ```bash
    Error: Command failed with exit code 125: podman inspect prometheus_pod-prometheus --format json
    Error: inspecting object: no such object: "prometheus_pod-prometheus"
    ```
    I've seen it could be a problem related to the MacOS setup, so I wanted to double check this.
