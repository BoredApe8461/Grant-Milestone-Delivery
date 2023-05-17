# Evaluation

- **Status:** Accepted
- **Application Document:** https://github.com/w3f/Grants-Program/blob/master/applications/GenesisDAO.md
- **Milestone:** 2
- **Kusama Identity:** Address
- **Previously successfully merged evaluation:** N/A

| Number | Deliverable | Accepted | Link | Evaluation Notes |
| ------ | ----------- | -------- | ---- |----------------- |
| 0a. | Licence |<ul><li>[x] </li></ul>| n/a |  | 
| 0b. | Documentation |<ul><li>[x] </li></ul>| n/a |  | 
| 0c. | Testing and Testing Guide |<ul><li>[x] </li></ul>| https://github.com/deep-ink-ventures/genesis-dao-node/blob/main/docs/testing.md |  |
| 0d. | Docker |<ul><li>[x] </li></ul>| [node Dockerfile](https://github.com/deep-ink-ventures/genesis-dao-node/blob/main/Dockerfile), [frontend Dockerfile](https://github.com/deep-ink-ventures/genesis-dao-frontend/blob/main/Dockerfile), [backend Dockerfile](https://github.com/deep-ink-ventures/genesis-dao-service/blob/main/Dockerfile) |  |
| 1. | Substrate module: pallet_dao_asset |<ul><li>[x] </li></ul>| [pallet](https://github.com/deep-ink-ventures/genesis-dao-node/tree/main/pallets/dao-assets) with [checkpoint functionality](https://github.com/deep-ink-ventures/genesis-dao-node/blob/main/pallets/dao-assets/src/functions.rs#L56-L130) |  |
| 2. | Substrate module: pallet_dao_vote	|<ul><li>[x] </li></ul>| https://github.com/deep-ink-ventures/genesis-dao-node/tree/main/pallets/dao-votes |  | 
| 3. | Frontend Implementation	 |<ul><li>[x] </li></ul>| https://genesis-dao.org |  |
| 4. | Design and Product Flow |<ul><li>[x] </li></ul>| https://github.com/deep-ink-ventures/genesis-dao-frontend/blob/main/design/Proposal.pdf |  |

## Evaluation V5

### Testing

I tested the application using docker again. This time I was able to start the node, service, and frontend without problems, create a DAO using the frontend and check the process in the node. I only noticed one minor problem, the image I uploaded wasn't showing in the DAO.

The problem that I had to start the service without docker seems to be in my environment and not a problem with the application since the docker is running fine.

I have tested pallet_dao_asset and pallet_dao_vote before, and they worked fine.

## Evaluation V4

### Docker

I tested the docker and got again the same error, but I was able to solve this by modifying the files:

Dockerfile
```
RUN rustup install nightly-2023-03-13-x86_64-unknown-linux-gnu 
RUN rustup default nightly-2023-03-13-x86_64-unknown-linux-gnu 
RUN rustup target add wasm32-unknown-unknown
RUN cargo build --release --features local-node
```

docker-compose.yml
```
services:
  chain:
    build: .
    ports:
      - "9944:9944"
    environment:
      - CARGO_HOME=/var/www/genesis-dao/.cargo
```

And with this, Docker started the node, service, and front end. But it doesn't seem to be connected. I tried to connect my wallet and received the error "n.balance is undefined", seems to be the same error I received trying without docker "account.balance is undefined".

I checked the containers and genesis-dao-node-listener-1 has some problems.
```
user@localhost:~/Documents/genesisdao/genesis-dao-node$ docker ps
CONTAINER ID   IMAGE                     COMMAND                  CREATED          STATUS          PORTS                                       NAMES
035b9fb73085   genesis-dao-node-web      "docker-entrypoint.s…"   22 seconds ago   Up 19 seconds   0.0.0.0:3000->3000/tcp, :::3000->3000/tcp   genesis-dao-node-web-1
07c94345eab7   genesis-dao-node-worker   "./entrypoint.sh wor…"   22 seconds ago   Up 20 seconds                                               genesis-dao-node-worker-1
337dd21213be   genesis-dao-node-app      "./entrypoint.sh web"    22 seconds ago   Up 20 seconds   0.0.0.0:8000->8000/tcp, :::8000->8000/tcp   genesis-dao-node-app-1
283cfb219d40   postgres:14.1-alpine      "docker-entrypoint.s…"   22 seconds ago   Up 21 seconds   0.0.0.0:5433->5432/tcp, :::5433->5432/tcp   genesis-dao-node-db-1
1ee29e7ce2c4   genesis-dao-node-chain    "./target/release/ge…"   22 seconds ago   Up 21 seconds   0.0.0.0:9944->9944/tcp, :::9944->9944/tcp   genesis-dao-node-chain-1
d99b68c5bf16   redis:5-alpine            "docker-entrypoint.s…"   22 seconds ago   Up 21 seconds   0.0.0.0:6379->6379/tcp, :::6379->6379/tcp   genesis-dao-node-cache-1
```
```
user@localhost:~/Documents/genesisdao/genesis-dao-node$ docker ps -a
CONTAINER ID   IMAGE                       COMMAND                  CREATED          STATUS                      PORTS                                       NAMES
035b9fb73085   genesis-dao-node-web        "docker-entrypoint.s…"   25 seconds ago   Up 22 seconds               0.0.0.0:3000->3000/tcp, :::3000->3000/tcp   genesis-dao-node-web-1
07c94345eab7   genesis-dao-node-worker     "./entrypoint.sh wor…"   25 seconds ago   Up 23 seconds                                                           genesis-dao-node-worker-1
337dd21213be   genesis-dao-node-app        "./entrypoint.sh web"    25 seconds ago   Up 23 seconds               0.0.0.0:8000->8000/tcp, :::8000->8000/tcp   genesis-dao-node-app-1
3e08c11c762d   genesis-dao-node-listener   "./entrypoint.sh lis…"   25 seconds ago   Exited (1) 20 seconds ago                                               genesis-dao-node-listener-1
283cfb219d40   postgres:14.1-alpine        "docker-entrypoint.s…"   25 seconds ago   Up 24 seconds               0.0.0.0:5433->5432/tcp, :::5433->5432/tcp   genesis-dao-node-db-1
1ee29e7ce2c4   genesis-dao-node-chain      "./target/release/ge…"   25 seconds ago   Up 24 seconds               0.0.0.0:9944->9944/tcp, :::9944->9944/tcp   genesis-dao-node-chain-1
d99b68c5bf16   redis:5-alpine              "docker-entrypoint.s…"   25 seconds ago   Up 24 seconds               0.0.0.0:6379->6379/tcp, :::6379->6379/tcp   genesis-dao-node-cache-1
```
```
user@localhost:~/Documents/genesisdao/genesis-dao-node$ docker logs genesis-dao-node-listener-1 
Syncing initial accounts...
Traceback (most recent call last):
  File "/venv/lib/python3.11/site-packages/django/db/backends/utils.py", line 89, in _execute
    return self.cursor.execute(sql, params)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
psycopg2.errors.UndefinedTable: relation "core_account" does not exist
LINE 1: INSERT INTO "core_account" ("created_at", "updated_at", "add...
                    ^
The above exception was the direct cause of the following exception:
Traceback (most recent call last):
  File "/usr/src/app/manage.py", line 22, in <module>
    main()
  File "/usr/src/app/manage.py", line 18, in main
    execute_from_command_line(sys.argv)
  File "/venv/lib/python3.11/site-packages/django/core/management/__init__.py", line 446, in execute_from_command_line
    utility.execute()
  File "/venv/lib/python3.11/site-packages/django/core/management/__init__.py", line 440, in execute
    self.fetch_command(subcommand).run_from_argv(self.argv)
  File "/venv/lib/python3.11/site-packages/django/core/management/base.py", line 402, in run_from_argv
    self.execute(*args, **cmd_options)
  File "/venv/lib/python3.11/site-packages/django/core/management/base.py", line 448, in execute
    output = self.handle(*args, **options)
             ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File "/usr/src/app/core/management/commands/blockchain_event_listener.py", line 8, in handle
    substrate_service.sync_initial_accs()  # todo check which data to preload
    ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File "/usr/src/app/core/substrate.py", line 133, in sync_initial_accs
    models.Account.objects.bulk_create(
  File "/venv/lib/python3.11/site-packages/django/db/models/manager.py", line 85, in manager_method
    return getattr(self.get_queryset(), name)(*args, **kwargs)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File "/venv/lib/python3.11/site-packages/django/db/models/query.py", line 799, in bulk_create
    returned_columns = self._batched_insert(
                       ^^^^^^^^^^^^^^^^^^^^^
  File "/venv/lib/python3.11/site-packages/django/db/models/query.py", line 1825, in _batched_insert
    self._insert(
  File "/venv/lib/python3.11/site-packages/django/db/models/query.py", line 1791, in _insert
    return query.get_compiler(using=using).execute_sql(returning_fields)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File "/venv/lib/python3.11/site-packages/django/db/models/sql/compiler.py", line 1660, in execute_sql
    cursor.execute(sql, params)
  File "/venv/lib/python3.11/site-packages/django/db/backends/utils.py", line 67, in execute
    return self._execute_with_wrappers(
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File "/venv/lib/python3.11/site-packages/django/db/backends/utils.py", line 80, in _execute_with_wrappers
    return executor(sql, params, many, context)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File "/venv/lib/python3.11/site-packages/django/db/backends/utils.py", line 84, in _execute
    with self.db.wrap_database_errors:
  File "/venv/lib/python3.11/site-packages/django/db/utils.py", line 91, in __exit__
    raise dj_exc_value.with_traceback(traceback) from exc_value
  File "/venv/lib/python3.11/site-packages/django/db/backends/utils.py", line 89, in _execute
    return self.cursor.execute(sql, params)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
django.db.utils.ProgrammingError: relation "core_account" does not exist
LINE 1: INSERT INTO "core_account" ("created_at", "updated_at", "add...
```

The logs from genesis-dao-node-db-1 seem to have some problem with Alice's address
```
user@localhost:~/Documents/genesisdao/genesis-dao-node$ docker logs genesis-dao-node-db-1
The files belonging to this database system will be owned by user "postgres".
This user must also own the server process.
The database cluster will be initialized with locale "en_US.utf8".
The default database encoding has accordingly been set to "UTF8".
The default text search configuration will be set to "english".
Data page checksums are disabled.
fixing permissions on existing directory /var/lib/postgresql/data ... ok
creating subdirectories ... ok
selecting dynamic shared memory implementation ... posix
selecting default max_connections ... 100
selecting default shared_buffers ... 128MB
selecting default time zone ... UTC
creating configuration files ... ok
running bootstrap script ... ok
sh: locale: not found
2023-04-27 15:51:13.304 UTC [30] WARNING:  no usable system locales were found
performing post-bootstrap initialization ... ok
syncing data to disk ... ok
Success. You can now start the database server using:
	pg_ctl -D /var/lib/postgresql/data -l logfile start
initdb: warning: enabling "trust" authentication for local connections
You can change this by editing pg_hba.conf or using the option -A, or
--auth-local and --auth-host, the next time you run initdb.
waiting for server to start....2023-04-27 15:51:13.944 UTC [36] LOG:  starting PostgreSQL 14.1 on x86_64-pc-linux-musl, compiled by gcc (Alpine 10.3.1_git20211027) 10.3.1 20211027, 64-bit
2023-04-27 15:51:13.946 UTC [36] LOG:  listening on Unix socket "/var/run/postgresql/.s.PGSQL.5432"
2023-04-27 15:51:13.951 UTC [37] LOG:  database system was shut down at 2023-04-27 15:51:13 UTC
2023-04-27 15:51:13.955 UTC [36] LOG:  database system is ready to accept connections
 done
server started
CREATE DATABASE
/usr/local/bin/docker-entrypoint.sh: ignoring /docker-entrypoint-initdb.d/*
waiting for server to shut down....2023-04-27 15:51:14.125 UTC [36] LOG:  received fast shutdown request
2023-04-27 15:51:14.126 UTC [36] LOG:  aborting any active transactions
2023-04-27 15:51:14.127 UTC [36] LOG:  background worker "logical replication launcher" (PID 43) exited with exit code 1
2023-04-27 15:51:14.127 UTC [38] LOG:  shutting down
2023-04-27 15:51:14.140 UTC [36] LOG:  database system is shut down
 done
server stopped
PostgreSQL init process complete; ready for start up.
2023-04-27 15:51:14.243 UTC [1] LOG:  starting PostgreSQL 14.1 on x86_64-pc-linux-musl, compiled by gcc (Alpine 10.3.1_git20211027) 10.3.1 20211027, 64-bit
2023-04-27 15:51:14.243 UTC [1] LOG:  listening on IPv4 address "0.0.0.0", port 5432
2023-04-27 15:51:14.243 UTC [1] LOG:  listening on IPv6 address "::", port 5432
2023-04-27 15:51:14.247 UTC [1] LOG:  listening on Unix socket "/var/run/postgresql/.s.PGSQL.5432"
2023-04-27 15:51:14.251 UTC [50] LOG:  database system was shut down at 2023-04-27 15:51:14 UTC
2023-04-27 15:51:14.256 UTC [1] LOG:  database system is ready to accept connections
2023-04-27 15:51:15.409 UTC [58] ERROR:  relation "core_account" does not exist at character 13
2023-04-27 15:51:15.409 UTC [58] STATEMENT:  INSERT INTO "core_account" ("created_at", "updated_at", "address") VALUES ('2023-04-27T15:51:15.409408+00:00'::timestamptz, '2023-04-27T15:51:15.409426+00:00'::timestamptz, '5GNJqTPyNqANBkUVMN1LPPrxXnFouWXoe2wNSmmEoLctxiZY'), ('2023-04-27T15:51:15.409440+00:00'::timestamptz, '2023-04-27T15:51:15.409446+00:00'::timestamptz, '5FHneW46xGXgs5mUiveU4sbTyGBzmstUspZC92UhjJM694ty'), ('2023-04-27T15:51:15.409455+00:00'::timestamptz, '2023-04-27T15:51:15.409462+00:00'::timestamptz, '5HpG9w8EBLe5XCrbczpwq5TSXvedjrBGCwqxK1iQ7qUsSWFc'), ('2023-04-27T15:51:15.409471+00:00'::timestamptz, '2023-04-27T15:51:15.409476+00:00'::timestamptz, '5GrwvaEF5zXb26Fz9rcQpDWS57CtERHpNehXCPcNoHGKutQY') ON CONFLICT DO NOTHING
```

### Without Docker

I had the same problems with service. I got this error using the command `pre-commit install` from `make build`.

```
user@localhost:~/Documents/genesisdao/genesis-dao-service$    pre-commit install
Traceback (most recent call last):
  File "/home/user/.local/bin/pre-commit", line 5, in <module>
    from pre_commit.main import main
  File "/home/user/.local/lib/python3.11/site-packages/pre_commit/main.py", line 12, in <module>
    from pre_commit.commands.autoupdate import autoupdate
  File "/home/user/.local/lib/python3.11/site-packages/pre_commit/commands/autoupdate.py", line 19, in <module>
    from pre_commit.store import Store
  File "/home/user/.local/lib/python3.11/site-packages/pre_commit/store.py", line 6, in <module>
    import sqlite3
  File "/usr/local/lib/python3.11/sqlite3/__init__.py", line 57, in <module>
    from sqlite3.dbapi2 import *
  File "/usr/local/lib/python3.11/sqlite3/dbapi2.py", line 27, in <module>
    from _sqlite3 import *
ModuleNotFoundError: No module named '_sqlite3'
```


## Evaluation V3


I still with the same problem for running the node using docker:

```
genesis-dao  | error: failed to run custom build command for `local-runtime v4.0.0-dev (/var/www/genesis-dao/runtime/local)`
genesis-dao  |
genesis-dao  | Caused by:
genesis-dao  |   process didn't exit successfully: `/var/www/genesis-dao/target/release/build/local-runtime-220d662ede7528cd/build-script-build` (exit status: 1)
genesis-dao  |   --- stderr
genesis-dao  |   Rust WASM toolchain not installed, please install it!
genesis-dao  |
genesis-dao  |   Further error information:
genesis-dao  |   ------------------------------------------------------------
genesis-dao  |  	Compiling wasm-test v1.0.0 (/tmp/.tmpcNlA6a)
genesis-dao  |   error[E0463]: can't find crate for `std`
genesis-dao  | 	|
genesis-dao  | 	= note: the `wasm32-unknown-unknown` target may not be installed
genesis-dao  | 	= help: consider downloading the target with `rustup target add wasm32-unknown-unknown`
genesis-dao  | 	= help: consider building the standard library from source with `cargo build -Zbuild-std`
genesis-dao  |
genesis-dao  |   error: cannot find macro `println` in this scope
genesis-dao  |	--> src/main.rs:3:5
genesis-dao  | 	|
genesis-dao  |   3 |             	println!("{}", env!("RUSTC_VERSION"));
genesis-dao  | 	|             	^^^^^^^
genesis-dao  |
genesis-dao  |   error: requires `sized` lang_item
genesis-dao  |
genesis-dao  |   For more information about this error, try `rustc --explain E0463`.
genesis-dao  |   error: could not compile `wasm-test` due to 3 previous errors
genesis-dao  |   ------------------------------------------------------------
genesis-dao  |
genesis-dao  | warning: build failed, waiting for other jobs to finish...
genesis-dao exited with code 101
```

### Service

This time, running the service with docker and using the external node worked well but when I tried to use the local node it failed to connect.

```
listener  | ConnectionRefusedError while initializing blockchain connection. Retrying in 10s ...
listener  | ConnectionRefusedError while initializing blockchain connection. Retrying in 30s ...
listener  | ConnectionRefusedError while initializing blockchain connection. Retrying in 60s ...
```

The ideal scenario would be to run the service with the node using docker. I tested without docker and got this error running `make build`:

```
pre-commit install
Traceback (most recent call last):
  File "/home/user/.local/bin/pre-commit", line 5, in <module>
	from pre_commit.main import main
  File "/home/user/.local/lib/python3.11/site-packages/pre_commit/main.py", line 12, in <module>
	from pre_commit.commands.autoupdate import autoupdate
  File "/home/user/.local/lib/python3.11/site-packages/pre_commit/commands/autoupdate.py", line 19, in <module>
	from pre_commit.store import Store
  File "/home/user/.local/lib/python3.11/site-packages/pre_commit/store.py", line 6, in <module>
	import sqlite3
  File "/usr/local/lib/python3.11/sqlite3/__init__.py", line 57, in <module>
	from sqlite3.dbapi2 import *
  File "/usr/local/lib/python3.11/sqlite3/dbapi2.py", line 27, in <module>
	from _sqlite3 import *
ModuleNotFoundError: No module named '_sqlite3'
make: *** [Makefile:11: build] Error 1
```

This error seems to be a dependency one. Instructions are saying that Python 3.11 is required with some dependencies but there is no script for doing the installation or at least links for where the user can find how to install them. I thought that was trivial for installing this, however after getting this problem for a while I think would be better to have instructions to install the dependencies for the project, including Python 3.11 and the libs required, such as sqlite3.


I could start the service, but it doesn't seams to be connected with the node. When I tried to connect my wallet in the frontend these logs appeared in the service, including the 404 code for some requests:

```
HTTP GET /accounts/?limit=5&offset=10 200 [0.02, 127.0.0.1:39216]
HTTP GET /static/rest_framework/css/bootstrap.min.css.map 304 [0.00, 127.0.0.1:39226]
HTTP GET /static/drf-yasg/redoc/redoc.standalone.js.map 304 [0.00, 127.0.0.1:39226]
HTTP GET /accounts/5DhZhZ5swfbobJMkcpYEm45aHa8LWyCkXGtjYBjKVPekQacw/ 404 [0.02, 127.0.0.1:39250]
HTTP GET /accounts/5DhZhZ5swfbobJMkcpYEm45aHa8LWyCkXGtjYBjKVPekQacw/ 404 [0.02, 127.0.0.1:39250]
```

## Evaluation V2

### Docker

I still have the same problems with Docker for the node and service. This time, the `listener` service started but still have errors with `worker` one. I tried to visit `http://127.0.0.1:8000/redoc/` and got a blank page.

```
worker	| Operations to perform:
worker	|   Apply all migrations: admin, auth, contenttypes, core, sessions
worker	| Running migrations:
worker	|   No migrations to apply.
listener  | Syncing initial accounts...
worker	| Traceback (most recent call last):
worker	|   File "/usr/src/app/manage.py", line 22, in <module>
worker	| 	main()
worker	|   File "/usr/src/app/manage.py", line 18, in main
worker	| 	execute_from_command_line(sys.argv)
worker	|   File "/venv/lib/python3.11/site-packages/django/core/management/__init__.py", line 446, in execute_from_command_line
worker	| 	utility.execute()
worker	|   File "/venv/lib/python3.11/site-packages/django/core/management/__init__.py", line 440, in execute
worker	| 	self.fetch_command(subcommand).run_from_argv(self.argv)
worker	|   File "/venv/lib/python3.11/site-packages/django/core/management/base.py", line 402, in run_from_argv
worker	| 	self.execute(*args, **cmd_options)
worker	|   File "/venv/lib/python3.11/site-packages/django/core/management/base.py", line 448, in execute
worker	| 	output = self.handle(*args, **options)
worker	|          	^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
worker	|   File "/venv/lib/python3.11/site-packages/django/contrib/staticfiles/management/commands/collectstatic.py", line 209, in handle
worker	| 	collected = self.collect()
worker	|             	^^^^^^^^^^^^^^
worker	|   File "/venv/lib/python3.11/site-packages/django/contrib/staticfiles/management/commands/collectstatic.py", line 135, in collect
worker	| 	handler(path, prefixed_path, storage)
worker	|   File "/venv/lib/python3.11/site-packages/django/contrib/staticfiles/management/commands/collectstatic.py", line 378, in copy_file
worker	| 	self.storage.save(prefixed_path, source_file)
worker	|   File "/venv/lib/python3.11/site-packages/django/core/files/storage.py", line 56, in save
worker	| 	name = self._save(name, content)
worker	|        	^^^^^^^^^^^^^^^^^^^^^^^^^
worker	|   File "/venv/lib/python3.11/site-packages/django/core/files/storage.py", line 295, in _save
worker	| 	os.makedirs(directory, exist_ok=True)
worker	|   File "<frozen os>", line 215, in makedirs
worker	|   File "<frozen os>", line 215, in makedirs
worker	|   File "<frozen os>", line 225, in makedirs
worker	| PermissionError: [Errno 13] Permission denied: '/usr/src/app/static'
worker exited with code 1
listener  | Catching up | number: 0
listener  | Catching up | number: 1
listener  | Catching up | number: 2
listener  | Catching up | number: 3
```

### Service

I tried without Docker, and this time I received this error when I ran `make start-dev`:

```
(venv) user@localhost:~/Documents/genesisdao/genesis-dao-service$ make start-dev
Traceback (most recent call last):
  File "/home/user/Documents/genesisdao/genesis-dao-service/manage.py", line 22, in <module>
    main()
  File "/home/user/Documents/genesisdao/genesis-dao-service/manage.py", line 18, in main
    execute_from_command_line(sys.argv)
  File "/home/user/Documents/genesisdao/genesis-dao-service/venv/lib/python3.9/site-packages/django/core/management/__init__.py", line 446, in execute_from_command_line
    utility.execute()
  File "/home/user/Documents/genesisdao/genesis-dao-service/venv/lib/python3.9/site-packages/django/core/management/__init__.py", line 440, in execute
    self.fetch_command(subcommand).run_from_argv(self.argv)
  File "/home/user/Documents/genesisdao/genesis-dao-service/venv/lib/python3.9/site-packages/django/core/management/base.py", line 402, in run_from_argv
    self.execute(*args, **cmd_options)
  File "/home/user/Documents/genesisdao/genesis-dao-service/venv/lib/python3.9/site-packages/django/core/management/base.py", line 448, in execute
    output = self.handle(*args, **options)
  File "/home/user/Documents/genesisdao/genesis-dao-service/venv/lib/python3.9/site-packages/django/core/management/base.py", line 96, in wrapped
    res = handle_func(*args, **kwargs)
  File "/home/user/Documents/genesisdao/genesis-dao-service/venv/lib/python3.9/site-packages/django/core/management/commands/migrate.py", line 97, in handle
    self.check(databases=[database])
  File "/home/user/Documents/genesisdao/genesis-dao-service/venv/lib/python3.9/site-packages/django/core/management/base.py", line 475, in check
    all_issues = checks.run_checks(
  File "/home/user/Documents/genesisdao/genesis-dao-service/venv/lib/python3.9/site-packages/django/core/checks/registry.py", line 88, in run_checks
    new_errors = check(app_configs=app_configs, databases=databases)
  File "/home/user/Documents/genesisdao/genesis-dao-service/venv/lib/python3.9/site-packages/django/core/checks/urls.py", line 14, in check_url_config
    return check_resolver(resolver)
  File "/home/user/Documents/genesisdao/genesis-dao-service/venv/lib/python3.9/site-packages/django/core/checks/urls.py", line 24, in check_resolver
    return check_method()
  File "/home/user/Documents/genesisdao/genesis-dao-service/venv/lib/python3.9/site-packages/django/urls/resolvers.py", line 494, in check
    for pattern in self.url_patterns:
  File "/home/user/Documents/genesisdao/genesis-dao-service/venv/lib/python3.9/site-packages/django/utils/functional.py", line 57, in __get__
    res = instance.__dict__[self.name] = self.func(instance)
  File "/home/user/Documents/genesisdao/genesis-dao-service/venv/lib/python3.9/site-packages/django/urls/resolvers.py", line 715, in url_patterns
    patterns = getattr(self.urlconf_module, "urlpatterns", self.urlconf_module)
  File "/home/user/Documents/genesisdao/genesis-dao-service/venv/lib/python3.9/site-packages/django/utils/functional.py", line 57, in __get__
    res = instance.__dict__[self.name] = self.func(instance)
  File "/home/user/Documents/genesisdao/genesis-dao-service/venv/lib/python3.9/site-packages/django/urls/resolvers.py", line 708, in urlconf_module
    return import_module(self.urlconf_name)
  File "/usr/lib/python3.9/importlib/__init__.py", line 127, in import_module
    return _bootstrap._gcd_import(name[level:], package, level)
  File "<frozen importlib._bootstrap>", line 1030, in _gcd_import
  File "<frozen importlib._bootstrap>", line 1007, in _find_and_load
  File "<frozen importlib._bootstrap>", line 986, in _find_and_load_unlocked
  File "<frozen importlib._bootstrap>", line 680, in _load_unlocked
  File "<frozen importlib._bootstrap_external>", line 790, in exec_module
  File "<frozen importlib._bootstrap>", line 228, in _call_with_frames_removed
  File "/home/user/Documents/genesisdao/genesis-dao-service/service/urls.py", line 22, in <module>
    from core import urls as core_urls
  File "/home/user/Documents/genesisdao/genesis-dao-service/core/urls.py", line 4, in <module>
    from core import views
  File "/home/user/Documents/genesisdao/genesis-dao-service/core/views.py", line 15, in <module>
    from core import models, serializers
  File "/home/user/Documents/genesisdao/genesis-dao-service/core/serializers.py", line 143
    match vote.in_favor:
          ^
SyntaxError: invalid syntax
make: *** [Makefile:17: run-migration] Error 1
```

### Frontend

I was able to test the front end using the external node and service. The functions are working fine, I was able to create a DAO, Edit its metadata, and transfer some tokens. But I noticed the page with Review Details is missing. After the creation, the message "Congratulations!" was presented, and another message as well "Sorry, you are not the admin of [Dao Name]". This this last one I think should't be presented. 

## Evaluation V1


### License

The License in the genesis-dao-service repository is missing.

### Documentation

The readme in the root of the repositories needs instructions on how to run the system using docker. 

Please provide a `.env.example` and a testing guide with examples and expected results for the frontend.

### Docker

The docker is working for the frontend but has some problems with the node and service.

Node Logs:
```
genesis-dao  | error: failed to run custom build command for `local-runtime v4.0.0-dev (/var/www/genesis-dao/runtime/local)`
genesis-dao  |
genesis-dao  | Caused by:
genesis-dao  |   process didn't exit successfully: `/var/www/genesis-dao/target/release/build/local-runtime-220d662ede7528cd/build-script-build` (exit status: 1)
genesis-dao  |   --- stderr
genesis-dao  |   Rust WASM toolchain not installed, please install it!
genesis-dao  |
genesis-dao  |   Further error information:
genesis-dao  |   ------------------------------------------------------------
genesis-dao  |  	Compiling wasm-test v1.0.0 (/tmp/.tmpCoNSpM)
genesis-dao  |   error[E0463]: can't find crate for `std`
genesis-dao  | 	|
genesis-dao  | 	= note: the `wasm32-unknown-unknown` target may not be installed
genesis-dao  | 	= help: consider downloading the target with `rustup target add wasm32-unknown-unknown`
genesis-dao  | 	= help: consider building the standard library from source with `cargo build -Zbuild-std`
genesis-dao  |
genesis-dao  |   error: cannot find macro `println` in this scope
genesis-dao  |	--> src/main.rs:3:5
genesis-dao  | 	|
genesis-dao  |   3 |             	println!("{}", env!("RUSTC_VERSION"));
genesis-dao  | 	|             	^^^^^^^
genesis-dao  |
genesis-dao  |   error: requires `sized` lang_item
genesis-dao  |
genesis-dao  |   For more information about this error, try `rustc --explain E0463`.
genesis-dao  |   error: could not compile `wasm-test` due to 3 previous errors
genesis-dao  |   ------------------------------------------------------------
genesis-dao  |
genesis-dao  | warning: build failed, waiting for other jobs to finish...
genesis-dao exited with code 101
```

Service Logs:
```
user@localhost:~/Documents/genesisdao/genesis-dao-service$ docker compose up
[+] Running 4/0
 ✔ Container redis 	Created                                                                                                                                                                            	0.0s
 ✔ Container postgres  Created                                                                                                                                                                            	0.0s
 ✔ Container worker	Created                                                                                                                                                                            	0.0s
 ✔ Container app   	Created                                                                                                                                                                            	0.0s
Attaching to app, postgres, redis, worker
redis 	| 1:C 14 Apr 2023 14:25:52.926 # oO0OoO0OoO0Oo Redis is starting oO0OoO0OoO0Oo
redis 	| 1:C 14 Apr 2023 14:25:52.926 # Redis version=5.0.14, bits=64, commit=00000000, modified=0, pid=1, just started
redis 	| 1:C 14 Apr 2023 14:25:52.926 # Configuration loaded
redis 	| 1:M 14 Apr 2023 14:25:52.927 * Running mode=standalone, port=6379.
redis 	| 1:M 14 Apr 2023 14:25:52.927 # Server initialized
redis 	| 1:M 14 Apr 2023 14:25:52.927 # WARNING overcommit_memory is set to 0! Background save may fail under low memory condition. To fix this issue add 'vm.overcommit_memory = 1' to /etc/sysctl.conf and then reboot or run the command 'sysctl vm.overcommit_memory=1' for this to take effect.
redis 	| 1:M 14 Apr 2023 14:25:52.928 # WARNING you have Transparent Huge Pages (THP) support enabled in your kernel. This will create latency and memory usage issues with Redis. To fix this issue run the command 'echo never > /sys/kernel/mm/transparent_hugepage/enabled' as root, and add it to your /etc/rc.local in order to retain the setting after a reboot. Redis must be restarted after THP is disabled.
redis 	| 1:M 14 Apr 2023 14:25:52.928 * Ready to accept connections
postgres  |
postgres  | PostgreSQL Database directory appears to contain a database; Skipping initialization
postgres  |
postgres  | 2023-04-14 14:25:52.957 UTC [1] LOG:  starting PostgreSQL 14.1 on x86_64-pc-linux-musl, compiled by gcc (Alpine 10.3.1_git20211027) 10.3.1 20211027, 64-bit
postgres  | 2023-04-14 14:25:52.957 UTC [1] LOG:  listening on IPv4 address "0.0.0.0", port 5432
postgres  | 2023-04-14 14:25:52.957 UTC [1] LOG:  listening on IPv6 address "::", port 5432
postgres  | 2023-04-14 14:25:52.960 UTC [1] LOG:  listening on Unix socket "/var/run/postgresql/.s.PGSQL.5432"
postgres  | 2023-04-14 14:25:52.964 UTC [21] LOG:  database system was interrupted; last known up at 2023-04-14 13:58:29 UTC
postgres  | 2023-04-14 14:25:53.080 UTC [21] LOG:  database system was not properly shut down; automatic recovery in progress
postgres  | 2023-04-14 14:25:53.081 UTC [21] LOG:  redo starts at 0/16FB250
postgres  | 2023-04-14 14:25:53.085 UTC [21] LOG:  invalid record length at 0/17A6248: wanted 24, got 0
postgres  | 2023-04-14 14:25:53.085 UTC [21] LOG:  redo done at 0/17A6220 system usage: CPU: user: 0.00 s, system: 0.00 s, elapsed: 0.00 s
postgres  | 2023-04-14 14:25:53.120 UTC [1] LOG:  database system is ready to accept connections
app   	| 2023-04-14 14:25:54,796 INFO 	Starting server at tcp:port=8000:interface=0.0.0.0
app   	| 2023-04-14 14:25:54,797 INFO 	HTTP/2 support not enabled (install the http2 and tls Twisted extras)
app   	| 2023-04-14 14:25:54,797 INFO 	Configuring endpoint tcp:port=8000:interface=0.0.0.0
app   	| 2023-04-14 14:25:54,797 INFO 	Listening on TCP address 0.0.0.0:8000
worker	| Operations to perform:
worker	|   Apply all migrations: admin, auth, contenttypes, core, sessions
worker	| Running migrations:
worker	|   No migrations to apply.
worker	| Traceback (most recent call last):
worker	|   File "/usr/src/app/manage.py", line 22, in <module>
worker	| 	main()
worker	|   File "/usr/src/app/manage.py", line 18, in main
worker	| 	execute_from_command_line(sys.argv)
worker	|   File "/venv/lib/python3.11/site-packages/django/core/management/__init__.py", line 446, in execute_from_command_line
worker	| 	utility.execute()
worker	|   File "/venv/lib/python3.11/site-packages/django/core/management/__init__.py", line 440, in execute
worker	| 	self.fetch_command(subcommand).run_from_argv(self.argv)
worker	|   File "/venv/lib/python3.11/site-packages/django/core/management/base.py", line 402, in run_from_argv
worker	| 	self.execute(*args, **cmd_options)
worker	|   File "/venv/lib/python3.11/site-packages/django/core/management/base.py", line 448, in execute
worker	| 	output = self.handle(*args, **options)
worker	|          	^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
worker	|   File "/venv/lib/python3.11/site-packages/django/contrib/staticfiles/management/commands/collectstatic.py", line 209, in handle
worker	| 	collected = self.collect()
worker	|             	^^^^^^^^^^^^^^
worker	|   File "/venv/lib/python3.11/site-packages/django/contrib/staticfiles/management/commands/collectstatic.py", line 135, in collect
worker	| 	handler(path, prefixed_path, storage)
worker	|   File "/venv/lib/python3.11/site-packages/django/contrib/staticfiles/management/commands/collectstatic.py", line 378, in copy_file
worker	| 	self.storage.save(prefixed_path, source_file)
worker	|   File "/venv/lib/python3.11/site-packages/django/core/files/storage.py", line 56, in save
worker	| 	name = self._save(name, content)
worker	|        	^^^^^^^^^^^^^^^^^^^^^^^^^
worker	|   File "/venv/lib/python3.11/site-packages/django/core/files/storage.py", line 295, in _save
worker	| 	os.makedirs(directory, exist_ok=True)
worker	|   File "<frozen os>", line 215, in makedirs
worker	|   File "<frozen os>", line 215, in makedirs
worker	|   File "<frozen os>", line 225, in makedirs
worker	| PermissionError: [Errno 13] Permission denied: '/usr/src/app/static'
worker exited with code 1
```

### Automate Testing

The Unit tests and the integration tests passed, some with good coverage and other could be improved. 

Dao-Core
```
test result: ok. 7 passed; 0 failed; 0 ignored; 0 measured; 0 filtered out; finished in 0.80s
Apr 14 08:18:37.661  INFO cargo_tarpaulin::report: Coverage Results:
|| Tested/Total Lines:
|| node/src/chain_spec.rs: 0/2
|| node/src/rpc.rs: 0/5
|| pallets/dao-assets/src/benchmarking.rs: 0/32
|| pallets/dao-assets/src/functions.rs: 114/352
|| pallets/dao-assets/src/impl_fungibles.rs: 10/61
|| pallets/dao-assets/src/lib.rs: 17/102
|| pallets/dao-assets/src/types.rs: 0/2
|| pallets/dao-assets/src/weights.rs: 7/226
|| pallets/dao-core/src/benchmarking.rs: 0/14
|| pallets/dao-core/src/functions.rs: 4/6
|| pallets/dao-core/src/lib.rs: 82/96
|| pallets/dao-core/src/weights.rs: 0/32
|| pallets/dao-votes/src/benchmarking.rs: 0/48
|| pallets/dao-votes/src/lib.rs: 0/128
|| pallets/dao-votes/src/weights.rs: 0/20
||
20.78% coverage, 234/1126 lines covered
```

Dao-Assets
```
test result: ok. 29 passed; 0 failed; 0 ignored; 0 measured; 0 filtered out; finished in 0.30s
Apr 14 08:22:21.111  INFO cargo_tarpaulin::report: Coverage Results:
|| Tested/Total Lines:
|| node/src/chain_spec.rs: 0/2
|| node/src/rpc.rs: 0/5
|| pallets/dao-assets/src/benchmarking.rs: 0/32
|| pallets/dao-assets/src/functions.rs: 312/358
|| pallets/dao-assets/src/impl_fungibles.rs: 18/63
|| pallets/dao-assets/src/lib.rs: 76/102
|| pallets/dao-assets/src/types.rs: 2/2
|| pallets/dao-assets/src/weights.rs: 14/226
|| pallets/dao-core/src/benchmarking.rs: 0/14
|| pallets/dao-core/src/functions.rs: 0/6
|| pallets/dao-core/src/lib.rs: 0/88
|| pallets/dao-core/src/weights.rs: 0/16
|| pallets/dao-votes/src/benchmarking.rs: 0/48
|| pallets/dao-votes/src/lib.rs: 0/128
|| pallets/dao-votes/src/weights.rs: 0/20
||
38.02% coverage, 422/1110 lines covered
```

Dao-Vote
```
test result: ok. 7 passed; 0 failed; 0 ignored; 0 measured; 0 filtered out; finished in 0.10s
Apr 14 08:25:51.107  INFO cargo_tarpaulin::report: Coverage Results:
|| Tested/Total Lines:
|| node/src/chain_spec.rs: 0/2
|| node/src/rpc.rs: 0/5
|| pallets/dao-assets/src/benchmarking.rs: 0/32
|| pallets/dao-assets/src/functions.rs: 160/355
|| pallets/dao-assets/src/impl_fungibles.rs: 4/61
|| pallets/dao-assets/src/lib.rs: 11/102
|| pallets/dao-assets/src/types.rs: 2/2
|| pallets/dao-assets/src/weights.rs: 0/226
|| pallets/dao-core/src/benchmarking.rs: 0/14
|| pallets/dao-core/src/functions.rs: 3/6
|| pallets/dao-core/src/lib.rs: 44/96
|| pallets/dao-core/src/weights.rs: 0/32
|| pallets/dao-votes/src/benchmarking.rs: 0/48
|| pallets/dao-votes/src/lib.rs: 107/137
|| pallets/dao-votes/src/weights.rs: 0/40
||
28.58% coverage, 331/1158 lines covered
```

Integration Test
```
test result: ok. 1 passed; 0 failed; 0 ignored; 0 measured; 0 filtered out; finished in 230.26s
Apr 14 08:41:06.845  INFO cargo_tarpaulin::report: Coverage Results:
|| Tested/Total Lines:
|| integration-wrapper/src/lib.rs: 86/86
|| node/src/chain_spec.rs: 0/2
|| node/src/rpc.rs: 0/5
|| pallets/dao-assets/src/benchmarking.rs: 0/32
|| pallets/dao-assets/src/functions.rs: 0/331
|| pallets/dao-assets/src/impl_fungibles.rs: 0/59
|| pallets/dao-assets/src/lib.rs: 0/86
|| pallets/dao-assets/src/weights.rs: 0/113
|| pallets/dao-core/src/benchmarking.rs: 0/14
|| pallets/dao-core/src/functions.rs: 0/6
|| pallets/dao-core/src/lib.rs: 0/88
|| pallets/dao-core/src/weights.rs: 0/16
|| pallets/dao-votes/src/benchmarking.rs: 0/48
|| pallets/dao-votes/src/lib.rs: 0/128
|| pallets/dao-votes/src/weights.rs: 0/20
||
8.32% coverage, 86/1034 lines covered
```

I ran `yarn test` in the frontend, and all tests passed too.

### Manual Testing 

I tested following [this guide](https://github.com/deep-ink-ventures/genesis-dao-node/blob/main/docs/testing.md#manual-voting), and all these functions are working fine.

I ran the frontend without problems, but when I tried to create a dao got this message "Sorry you need at least 10 DOT tokens to create a DAO. You will get them back if you destroy the DAO.". Even that I get more balance for the connected account, the error msg remains.

I tried to run the services using docker and got the error mentioned above. So I tried to run without docker and got this error:
```
(venv) user@localhost:~/Documents/genesisdao/genesis-dao-service$ make start-dev
Operations to perform:
  Apply all migrations: admin, auth, contenttypes, core, sessions
Running migrations:
  No migrations to apply.
Watching for file changes with StatReloader
Performing system checks...
System check identified no issues (0 silenced).
April 14, 2023 - 14:32:42
Django version 4.1.7, using settings 'settings.settings'
Starting ASGI/Daphne version 4.0.0 development server at http://127.0.0.1:8000/
Quit the server with CONTROL-C.
Internal Server Error: /
Traceback (most recent call last):
  File "/home/user/Documents/genesisdao/genesis-dao-service/venv/lib/python3.9/site-packages/redis/connection.py", line 715, in connect
	sock = self.retry.call_with_retry(
  File "/home/user/Documents/genesisdao/genesis-dao-service/venv/lib/python3.9/site-packages/redis/retry.py", line 46, in call_with_retry
	return do()
  File "/home/user/Documents/genesisdao/genesis-dao-service/venv/lib/python3.9/site-packages/redis/connection.py", line 716, in <lambda>
	lambda: self._connect(), lambda error: self.disconnect(error)
  File "/home/user/Documents/genesisdao/genesis-dao-service/venv/lib/python3.9/site-packages/redis/connection.py", line 781, in _connect
	raise err
  File "/home/user/Documents/genesisdao/genesis-dao-service/venv/lib/python3.9/site-packages/redis/connection.py", line 769, in _connect
	sock.connect(socket_address)
ConnectionRefusedError: [Errno 111] Connection refused
During handling of the above exception, another exception occurred:
Traceback (most recent call last):
  File "/home/user/Documents/genesisdao/genesis-dao-service/venv/lib/python3.9/site-packages/asgiref/sync.py", line 486, in thread_handler
	raise exc_info[1]
  File "/home/user/Documents/genesisdao/genesis-dao-service/venv/lib/python3.9/site-packages/django/core/handlers/exception.py", line 43, in inner
	response = await get_response(request)
  File "/home/user/Documents/genesisdao/genesis-dao-service/venv/lib/python3.9/site-packages/django/utils/deprecation.py", line 154, in __acall__
	response = await sync_to_async(
  File "/home/user/Documents/genesisdao/genesis-dao-service/venv/lib/python3.9/site-packages/asgiref/sync.py", line 448, in __call__
	ret = await asyncio.wait_for(future, timeout=None)
  File "/usr/lib/python3.9/asyncio/tasks.py", line 442, in wait_for
	return await fut
  File "/usr/lib/python3.9/concurrent/futures/thread.py", line 52, in run
	result = self.fn(*self.args, **self.kwargs)
  File "/home/user/Documents/genesisdao/genesis-dao-service/venv/lib/python3.9/site-packages/asgiref/sync.py", line 490, in thread_handler
	return func(*args, **kwargs)
  File "/home/user/Documents/genesisdao/genesis-dao-service/core/middleware.py", line 16, in process_response
	if current_block := cache.get("current_block"):
  File "/home/user/Documents/genesisdao/genesis-dao-service/venv/lib/python3.9/site-packages/django/core/cache/backends/redis.py", line 187, in get
	return self._cache.get(key, default)
  File "/home/user/Documents/genesisdao/genesis-dao-service/venv/lib/python3.9/site-packages/django/core/cache/backends/redis.py", line 99, in get
	value = client.get(key)
  File "/home/user/Documents/genesisdao/genesis-dao-service/venv/lib/python3.9/site-packages/redis/commands/core.py", line 1790, in get
	return self.execute_command("GET", name)
  File "/home/user/Documents/genesisdao/genesis-dao-service/venv/lib/python3.9/site-packages/redis/client.py", line 1255, in execute_command
	conn = self.connection or pool.get_connection(command_name, **options)
  File "/home/user/Documents/genesisdao/genesis-dao-service/venv/lib/python3.9/site-packages/redis/connection.py", line 1481, in get_connection
	connection.connect()
  File "/home/user/Documents/genesisdao/genesis-dao-service/venv/lib/python3.9/site-packages/redis/connection.py", line 721, in connect
	raise ConnectionError(self._error_message(e))
redis.exceptions.ConnectionError: Error 111 connecting to 0.0.0.0:6379. Connection refused.
Internal Server Error: /
Traceback (most recent call last):
  File "/home/user/Documents/genesisdao/genesis-dao-service/venv/lib/python3.9/site-packages/redis/connection.py", line 715, in connect
	sock = self.retry.call_with_retry(
  File "/home/user/Documents/genesisdao/genesis-dao-service/venv/lib/python3.9/site-packages/redis/retry.py", line 46, in call_with_retry
	return do()
  File "/home/user/Documents/genesisdao/genesis-dao-service/venv/lib/python3.9/site-packages/redis/connection.py", line 716, in <lambda>
	lambda: self._connect(), lambda error: self.disconnect(error)
  File "/home/user/Documents/genesisdao/genesis-dao-service/venv/lib/python3.9/site-packages/redis/connection.py", line 781, in _connect
	raise err
  File "/home/user/Documents/genesisdao/genesis-dao-service/venv/lib/python3.9/site-packages/redis/connection.py", line 769, in _connect
	sock.connect(socket_address)
ConnectionRefusedError: [Errno 111] Connection refused
During handling of the above exception, another exception occurred:
Traceback (most recent call last):
  File "/home/user/Documents/genesisdao/genesis-dao-service/venv/lib/python3.9/site-packages/asgiref/sync.py", line 486, in thread_handler
	raise exc_info[1]
  File "/home/user/Documents/genesisdao/genesis-dao-service/venv/lib/python3.9/site-packages/django/core/handlers/exception.py", line 43, in inner
	response = await get_response(request)
  File "/home/user/Documents/genesisdao/genesis-dao-service/venv/lib/python3.9/site-packages/django/utils/deprecation.py", line 154, in __acall__
	response = await sync_to_async(
  File "/home/user/Documents/genesisdao/genesis-dao-service/venv/lib/python3.9/site-packages/asgiref/sync.py", line 448, in __call__
	ret = await asyncio.wait_for(future, timeout=None)
  File "/usr/lib/python3.9/asyncio/tasks.py", line 442, in wait_for
	return await fut
  File "/usr/lib/python3.9/concurrent/futures/thread.py", line 52, in run
	result = self.fn(*self.args, **self.kwargs)
  File "/home/user/Documents/genesisdao/genesis-dao-service/venv/lib/python3.9/site-packages/asgiref/sync.py", line 490, in thread_handler
	return func(*args, **kwargs)
  File "/home/user/Documents/genesisdao/genesis-dao-service/core/middleware.py", line 16, in process_response
	if current_block := cache.get("current_block"):
  File "/home/user/Documents/genesisdao/genesis-dao-service/venv/lib/python3.9/site-packages/django/core/cache/backends/redis.py", line 187, in get
	return self._cache.get(key, default)
  File "/home/user/Documents/genesisdao/genesis-dao-service/venv/lib/python3.9/site-packages/django/core/cache/backends/redis.py", line 99, in get
	value = client.get(key)
  File "/home/user/Documents/genesisdao/genesis-dao-service/venv/lib/python3.9/site-packages/redis/commands/core.py", line 1790, in get
	return self.execute_command("GET", name)
  File "/home/user/Documents/genesisdao/genesis-dao-service/venv/lib/python3.9/site-packages/redis/client.py", line 1255, in execute_command
	conn = self.connection or pool.get_connection(command_name, **options)
  File "/home/user/Documents/genesisdao/genesis-dao-service/venv/lib/python3.9/site-packages/redis/connection.py", line 1481, in get_connection
	connection.connect()
  File "/home/user/Documents/genesisdao/genesis-dao-service/venv/lib/python3.9/site-packages/redis/connection.py", line 721, in connect
	raise ConnectionError(self._error_message(e))
redis.exceptions.ConnectionError: Error 111 connecting to 0.0.0.0:6379. Connection refused.
HTTP GET / 500 [0.08, 127.0.0.1:57252]
```
