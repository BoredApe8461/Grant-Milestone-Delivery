# Evaluation

- **Status:** Accepted
- **Application Document:** https://github.com/w3f/Grants-Program/blob/master/applications/patron.md
- **Milestone:** 1
- **Kusama Identity:** Address
- **Previously successfully merged evaluation:** All by takahser

| Number | Deliverable | Accepted | Link | Evaluation Notes |
| ------ | ----------- | -------- | ---- |----------------- |
| 0a. | License | <ul><li>[x] </li></ul> | [MIT](https://github.com/Brushfam/patron-backend/blob/fcaefc0df32a58a58aa056ef5952223829f19ee7/LICENSE) | - |
| 0b. | Documentation | <ul><li>[x] </li></ul> | [CLI docs](https://github.com/Brushfam/patron-backend/blob/fcaefc0df32a58a58aa056ef5952223829f19ee7/docs/cli.md), [self-hosting instructions](https://github.com/Brushfam/patron-backend/blob/fcaefc0df32a58a58aa056ef5952223829f19ee7/docs/self-hosted.md), [API docs](https://api.patron.works/docs) | See [documentation feedback](#documentation-feedback). |
| 0c. | Testing guidelines | <ul><li>[x] </li></ul> | [Instructions in Delivery](https://github.com/w3f/Grant-Milestone-Delivery/pull/871/files#diff-c6776ce4032fba925481b56ba22f31870e3afd145b38a80d8854ab970066986bR25-R167) | See [testing guidelines feedback](#testing-guidelines-feedback). |
| 0d. | Docker |<ul><li>[x] </li></ul> | [containers.rs](https://github.com/Brushfam/patron-backend/blob/fcaefc0df32a58a58aa056ef5952223829f19ee7/crates/builder/src/process/container.rs) | See [Docker Feedback](#docker-feedback) |
| 0e. | Article | <ul><li>[x] </li></ul> | [Medium Article](https://medium.com/brushfam/patron-is-your-one-stop-smart-contract-manager-for-polkadot-ecosystem-b1f89a48ba40) | ~~Rather poorly written. I assume there hasn't been any proof-reading process. Given the price tag of this grant I think it'd be fair to expect a higher quality here.~~ Still not perfect, but drastically improved from the earlier version. I'm willing to accept it at this stage, however, feel free to further improve it. |
| 1a. | Backend storage | <ul><li>[x] </li></ul> | [db crate](https://github.com/Brushfam/patron-backend/tree/fcaefc0df32a58a58aa056ef5952223829f19ee7/crates/db) | See [backend storage feedback](#backend-storage-feedback). |
| 1b. | Sync server | <ul><li>[x] </li></ul> | [server crate](https://github.com/Brushfam/patron-backend/tree/d6bb21b010d4b9abf13c7ee7bce4b3898c3a1fc0/crates/server) | - |
| 1c. | Smart contract builder | <ul><li>[x] </li></ul> | [builder crate](https://github.com/Brushfam/patron-backend/tree/d6bb21b010d4b9abf13c7ee7bce4b3898c3a1fc0/crates/builder/src) | - |
| 2a. | Web UI | <ul><li>[x] </li></ul> | [patron frontend repo](https://github.com/Brushfam/patron-frontend/tree/master) | See [Web UI Feedback](#web-ui-feedback) |
| 2b. | Detailed contract information | <ul><li>[x] </li></ul> | [CodeHashWindow.tsx](https://github.com/Brushfam/patron-frontend/blob/f0a32db6ba72da3a4dc65034ec64e7ec7ce2f0b0/src/pages/CodeHashWindow.tsx) | - |
| 2c. | User authentication | <ul><li>[x] </li></ul> | [auth command](https://github.com/Brushfam/patron-backend/blob/d6bb21b010d4b9abf13c7ee7bce4b3898c3a1fc0/crates/patron/src/commands/auth.rs) | - |
| 3a. | Developer CLI utility | <ul><li>[x] </li></ul> | [patron crate](https://github.com/Brushfam/patron-backend/tree/d6bb21b010d4b9abf13c7ee7bce4b3898c3a1fc0/crates/patron) | - |


Ideally all links inside the above table should include the commit hash,
which was used for testing the delivery. It should also be checked if the software is published under the correct open-source license.

## General Notes

### Documentation Feedback

The spec in the proposal reads:

> We will provide API documentation for contributors to get along with the codebase, as well as a detailed self-hosting instructions for users to create their own nodes.

~~However, I couldn't find an "API documentation for contributors".
Also, the code has almost no inline comments, which makes it harder for contributers to understand the code. For reference you can have a look at some of parity pallets, e.g. the [assets pallet](https://github.com/paritytech/substrate/blob/e434882d5dbf3f3f6085cb7f1d017dbc4ac11f0a/frame/assets/src/lib.rs) for some inspiration on inline-comments. In a second step, you could use `rustdoc` to generate the documentation based on the inline comments you provided.~~

Update: inline-comments and [API docs](https://api.patron.works/docs) have been added

### Testing Guidelines Feedback

- [x] tests ~~currently fail~~ have been fixed:

     ```
     patron-backend % cargo test
     Compiling event_client v0.1.0 (/Users/xxx/repos/patron-backend/crates/event_client)
     Finished test [unoptimized + debuginfo] target(s) in 2m 52s
          Running unittests src/main.rs (target/debug/deps/builder-761d50c22f6d842b)

     running 0 tests

     test result: ok. 0 passed; 0 failed; 0 ignored; 0 measured; 0 filtered out; finished in 0.00s

          Running unittests src/lib.rs (target/debug/deps/common-e50cefc8408d0d31)

     running 0 tests

     test result: ok. 0 passed; 0 failed; 0 ignored; 0 measured; 0 filtered out; finished in 0.00s

          Running unittests src/lib.rs (target/debug/deps/db-5a50e7f8e8a774ec)

     running 1 test
     test tests::exists ... ok

     test result: ok. 1 passed; 0 failed; 0 ignored; 0 measured; 0 filtered out; finished in 0.01s

          Running unittests src/main.rs (target/debug/deps/event_client-39f93758411ef1f8)

     running 2 tests
     test utils::tests::extract_code_hash ... ok
     test utils::tests::extract_twox_account_id ... ok

     test result: ok. 2 passed; 0 failed; 0 ignored; 0 measured; 0 filtered out; finished in 0.00s

          Running unittests src/lib.rs (target/debug/deps/migration-32a0379cff62aa67)

     running 0 tests

     test result: ok. 0 passed; 0 failed; 0 ignored; 0 measured; 0 filtered out; finished in 0.00s

          Running unittests src/main.rs (target/debug/deps/migration-a6d13c5c9ea0a0e1)

     running 0 tests

     test result: ok. 0 passed; 0 failed; 0 ignored; 0 measured; 0 filtered out; finished in 0.00s

          Running unittests src/main.rs (target/debug/deps/patron-d1f0e973f6accda7)

     running 0 tests

     test result: ok. 0 passed; 0 failed; 0 ignored; 0 measured; 0 filtered out; finished in 0.00s

          Running unittests src/main.rs (target/debug/deps/server-a8daf5b4743e4bfd)

     running 37 tests
     test handlers::auth::login::tests::unmatching_signature ... ok
     test handlers::build_sessions::create::tests::create ... ok
     test handlers::auth::register::tests::register ... ok
     test handlers::auth::login::tests::invalid_signature ... ok
     test handlers::build_sessions::create::tests::invalid_source_code_id ... ok
     test handlers::auth::login::tests::invalid_account ... ok
     test handlers::auth::login::tests::missing_account ... ok
     test handlers::build_sessions::create::tests::invalid_version ... ok
     test handlers::build_sessions::details::tests::successful ... ok
     test handlers::auth::login::tests::cli_token_repetition ... ok
     test handlers::auth::login::tests::exchange ... ok
     test handlers::auth::login::tests::successful ... ok
     test handlers::build_sessions::metadata::tests::unknown ... ok
     test handlers::build_sessions::details::tests::unknown ... ok
     test handlers::build_sessions::list::tests::successful ... ok
     test handlers::build_sessions::logs::tests::successful_by_code_hash ... ok
     test handlers::build_sessions::status::tests::unknown ... ok
     test handlers::build_sessions::logs::tests::unknown ... ok
     test handlers::build_sessions::latest::tests::successful ... ok
     test handlers::build_sessions::logs::tests::position ... ok
     test handlers::build_sessions::metadata::tests::successful ... ok
     test handlers::build_sessions::latest::tests::source_code_without_build_sessions ... ok
     test handlers::build_sessions::status::tests::successful ... ok
     test handlers::build_sessions::logs::tests::successful_by_id ... ok
     test handlers::files::details::tests::file_list ... ok
     test handlers::contracts::events::tests::successful ... ok
     test handlers::files::upload::tests::upload_and_seal ... ok
     test handlers::keys::delete::tests::list_and_delete ... ok
     test handlers::files::details::tests::unknown_file ... ok
     test handlers::contracts::details::tests::unknown ... ok
     test handlers::build_sessions::wasm::tests::unknown ... ok
     test handlers::files::details::tests::single_file ... ok
     test handlers::files::upload::tests::empty_request ... ok
     test handlers::build_sessions::wasm::tests::successful ... ok
     test handlers::contracts::details::tests::successful ... ok
     test handlers::contracts::events::tests::unknown ... ok
     test handlers::keys::verify::tests::list_and_verify ... ok

     test result: ok. 37 passed; 0 failed; 0 ignored; 0 measured; 0 filtered out; finished in 0.50s

     Doc-tests common

     running 0 tests

     test result: ok. 0 passed; 0 failed; 0 ignored; 0 measured; 0 filtered out; finished in 0.00s

     Doc-tests db

     running 3 tests
     test src/lib.rs - SelectExt::exists (line 107) ... ignored
     test src/token.rs - token::generate_token (line 63) ... ok
     test src/lib.rs - TransactionErrorExt::into_raw_result (line 40) ... ok

     test result: ok. 2 passed; 0 failed; 1 ignored; 0 measured; 0 filtered out; finished in 1.45s

     Doc-tests migration

     running 0 tests

     test result: ok. 0 passed; 0 failed; 0 ignored; 0 measured; 0 filtered out; finished in 0.00s
     ```

### Docker Feedback

- linux install instructions for NIX have been [added](https://github.com/Brushfam/patron-backend/blob/master/docs/self-hosted.md#nix-installation)
- I followed the MacOS instructions on the [NIX webpage](https://nixos.org/download.html#nix-install-macos) but the install script tried to add at least 7 users to my local machine so I decided to not use it:

     ```bash
     ~~> Setting up the build user _nixbld7

     ---- sudo execution ------------------------------------------------------------
     I am executing:

     $ sudo /usr/bin/dscl . create /Users/_nixbld7 UniqueID 307

     Creating the Nix build user (#7), _nixbld7
     ```

- ~~there are no instructions for using docker without NIX, feel free to add those as well~~ => apparently there is no good way to use it on MacOS (although it's officially supported) since its usage relies heaviliy on linux-specific components that are not present on MacOS.
- ~~also, I didn't find any docker or docker-compose files except for the [containers.rs](https://github.com/Brushfam/patron-backend/blob/d6bb21b010d4b9abf13c7ee7bce4b3898c3a1fc0/crates/builder/src/process/container.rs) of which I'm not sure what exactly it does, feel free to add some more info there as well~~
- The docker containers are built dynamically and rely on linux-specific components such as `udisks2` which is why no hardcoded docker files have been added. While the CLI doesn't rely on linux-specific components it's still not possible to dockerize it for technical reasons.
- The instructions have been successfully tested on a Linux Ubuntu machine. This involved:
  - setting up the db
  - initialize the db using a remote (astar) node
  - query data on the local db, such as contracts and contract owner addresses
  - listen to incoming ink! smartcontract events
  - CLI, incl. authentication
  - upload and verification of a smart contract using the web ui

### Backend Storage Feedback

- regarding running the DB, ~~please add instructions on how to install and configure it so it matches your example *Config.toml* file mentioned in the [CLI docs](https://github.com/Brushfam/patron-backend/blob/fcaefc0df32a58a58aa056ef5952223829f19ee7/docs/self-hosted.md#configuration)~~ the [install instructions](https://github.com/Brushfam/patron-backend/blob/d6bb21b010d4b9abf13c7ee7bce4b3898c3a1fc0/docs/self-hosted.md#postgresql) and [an example config file](https://github.com/Brushfam/patron-backend/blob/d6bb21b010d4b9abf13c7ee7bce4b3898c3a1fc0/docs/self-hosted.md#configuration) have been added

- the build passes:

     ```bash
     % cargo build --release

     Compiling proc-macro2 v1.0.59
     Compiling quote v1.0.28
     
     (...)

     Compiling tar v0.4.38
     Compiling migration v0.1.0 (/Users/xxx/repos/patron-backend/crates/migration)
     Compiling validator v0.16.0
     Compiling ink_metadata v4.2.0
     Compiling serde_plain v1.0.1
     Compiling which v4.4.0
     Compiling zip v0.6.6
     Compiling axum-derive-error v0.1.0
     Compiling home v0.5.5
     Compiling patron v0.1.0 (/Users/xxx/repos/patron-backend/crates/patron)
     Compiling event_client v0.1.0 (/Users/xxx/repos/patron-backend/crates/event_client)
     Compiling server v0.1.0 (/Users/xxx/repos/patron-backend/crates/server)
     Compiling builder v0.1.0 (/Users/xxx/repos/patron-backend/crates/builder)
     Finished release [optimized] target(s) in 5m 15s
     ```

### Web UI Feedback

- [x] ~~there are currently a couple of npm vulnerabilities present. Please fix them or explain why they shouldn't or can't be fixed (if applicable)~~ The vulnerabilities have been fixed, except for the [known open issue in the create-react-app repo](https://github.com/facebook/create-react-app/issues/11174):

     ```bash
     patron-frontend % npm audit --omit=dev
     found 0 vulnerabilities
     ```

- [x] ~~The UI can be started successfully, but there are some warnings. Some can easily be fixed, for example this code in [AddressElements.tsx](https://github.com/Brushfam/patron-frontend/blob/f0a32db6ba72da3a4dc65034ec64e7ec7ce2f0b0/src/components/ContractComponents/AddressElements.tsx#L56): `<img src={props.name == "Address" ? "/icons/user.svg" : "/icons/contract-icon.svg"} alt={"user icon"} />`. Full excerpt:~~ => fixed


     ```bash
     patron-frontend % npm run start
     
     (...)

     Compiled successfully!

     You can now view patron-ui in the browser.

     Local:            http://localhost:3000
     On Your Network:  http://192.168.0.101:3000

     Note that the development build is not optimized.
     To create a production build, use npm run build.

     webpack compiled successfully
     No issues found.
     One of your dependencies, babel-preset-react-app, is importing the
     "@babel/plugin-proposal-private-property-in-object" package without
     declaring it in its dependencies. This is currently working because
     "@babel/plugin-proposal-private-property-in-object" is already in your
     node_modules folder for unrelated reasons, but it may break at any time.

     babel-preset-react-app is part of the create-react-app project, which
     is not maintianed anymore. It is thus unlikely that this bug will
     ever be fixed. Add "@babel/plugin-proposal-private-property-in-object" to
     your devDependencies to work around this error. This will make this message
     go away.
     ```
