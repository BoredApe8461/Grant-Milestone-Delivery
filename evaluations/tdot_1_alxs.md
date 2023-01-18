# Evaluation

- **Status:** Accepted
- **Application Document:** https://github.com/w3f/Grants-Program/blob/master/applications/tdot.md
- **Milestone:** 1

| Number | Deliverable | Accepted | Link | Evaluation Notes |
| ------ | ----------- | -------- | ---- |----------------- |
| 0a. | License | <ul><li>[x] </li></ul> | [LICENSE](https://github.com/nutsfinance/stable-asset/blob/e5c8c1ba19c730257e01077ce1c326476c1002c2/LICENSE) | Apache 2.0 |
| 0b. | Documentation | <ul><li>[x] </li></ul> | [external docs](https://nutsfinance.gitbook.io/) ([github](https://github.com/nutsfinance/nutsfinance.github.io)), [architecture section](https://nutsfinance.gitbook.io/tapio/overview/architecture) | diagrams initially mentioned in application added to it |
| 0c.  | Testing | <ul><li>[x] </li></ul> |[tests](https://github.com/nutsfinance/stable-asset/blob/e5c8c1ba19c730257e01077ce1c326476c1002c2/lib/stable-asset-xcm/src/tests.rs#L40-L156)| improved |
| 0d.  | Docker | <ul><li>[x] </li></ul> |[Acala](https://github.com/AcalaNetwork/Acala/blob/ad240e9b96d4338a66fe7daad5bf53d8bb6a25f8/scripts/Dockerfile), [bifrost](https://github.com/nutsfinance/bifrost/blob/f0cba77760cf7e9b4576f6a255c6496edd36aad0/Dockerfile), [stable-asset](https://github.com/nutsfinance/stable-asset/blob/e5c8c1ba19c730257e01077ce1c326476c1002c2/Dockerfile) | accompanying Dockerfile (last item) does not utilise XCM functionality |
| 1.  | Substrate module: Stable Asset XCM | <ul><li>[x] </li></ul> |[code](https://github.com/nutsfinance/stable-asset/blob/e5c8c1ba19c730257e01077ce1c326476c1002c2/lib/stable-asset-xcm/src/lib.rs) | |

## General Notes

Readable code and good external documentation, great communication with team.

Inline documentation present but sparse and could be improved.
`cargo clippy` comes back clean.

Test coverage high enough - the application nevertheless specified "comprehensive tests" and the initial delivery contained barely a few, e.g. 3 for this milestone.
The team improved this in response to feedback with final test coverage at around 89%.
