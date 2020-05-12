DDEV Config for Newsroom

Changes to web service are in ./web-build,

In this ddev config I disabled db and dba services, check docker-compose.override.yaml, this causes a error when we run ddev start, just ignore.


When starting ddev after images being pullded, you must wait some minutes to let oracle database initialization finish, use "ddev logs -fs oracle"
