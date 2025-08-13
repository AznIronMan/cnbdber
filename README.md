CNBDBer

Universal DB runner for SQL-like commands across SQLite, MySQL, PostgreSQL, and MongoDB.

Install

- From PyPI (Python 3.9+):
```bash
pip install cnbdber
# optional extras
pip install 'cnbdber[mysql]'
pip install 'cnbdber[postgres]'
pip install 'cnbdber[mongo]'
```
- From source (development):
```bash
pip install -e .
```

Config

- App config: `./.configs/cnbdber.config` (auto-created on first run)
- Logger config: `./.configs/cnblogger.config` (auto-created if missing)
- Logs: `./.logs/`

You can override the app config via `CNBDBER_CONFIG=/abs/path/to/cnbdber.config`.
The logger path is read from `cnbdber.config` and passed directly to `CNBLogger`.

Usage

Run a one-off command:
```bash
cnbdber -c "SELECT * FROM users LIMIT 5;"
```
Run from a file:
```bash
cnbdber --file ./query.sql
```
Specify a config explicitly:
```bash
cnbdber --config ./my-config.json -c "DELETE FROM logs WHERE created_at < NOW() - INTERVAL 30 DAY;"
```

- SQL backends (SQLite/MySQL/PostgreSQL): raw SQL is executed as-is.
- MongoDB: a minimal SQL-to-Mongo translation is supported for simple `SELECT/INSERT/UPDATE/DELETE` with equality-only `WHERE` clauses.

Example cnbdber.config

```json
{
  "logger_config_path": "./.configs/cnblogger.config",
  "target": {
    "type": "sqlite",
    "sqlite_path": "./example.db"
  }
}
```

Switch to MySQL:
```json
{
  "logger_config_path": "./.configs/cnblogger.config",
  "target": {
    "type": "mysql",
    "host": "127.0.0.1",
    "port": 3306,
    "user": "root",
    "password": "",
    "database": "test"
  }
}
```

License

MIT


