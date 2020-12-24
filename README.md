# Self Hosted CI/CD Setup

A note for self hosted cicd setup, using docker, gitea, drone.

## Git server

[Gitea](https://github.com/go-gitea/gitea)

My configurations [below](#gitea-full-config), for more at https://docs.gitea.io/en-us/config-cheat-sheet/

## Drone

Follow the setup guide [here](https://docs.drone.io/server/provider/gitea/),  
and replace the environment variables in the docker-compose file.

## Examples

For examples that need host docker support, the repo must be marked trusted by the admin.


## Gitea full config

```ini
# data/gitea/conf/app.ini
APP_NAME = Evan Repo
RUN_MODE = prod
RUN_USER = git

[repository]
ROOT = /data/git/repositories

[repository.local]
LOCAL_COPY_PATH = /data/gitea/tmp/local-repo

[repository.upload]
TEMP_PATH = /data/gitea/uploads

[server]
APP_DATA_PATH    = /data/gitea
DOMAIN           = HOST_NAME
SSH_DOMAIN       = HOST_NAME
HTTP_PORT        = 3000
ROOT_URL         = https:/HOST_NAME/
DISABLE_SSH      = false
SSH_PORT         = 10022
SSH_LISTEN_PORT  = 22
LFS_START_SERVER = true
LFS_CONTENT_PATH = /data/git/lfs
LFS_JWT_SECRET   = SECRET
OFFLINE_MODE     = false

[database]
PATH     = /data/gitea/gitea.db
DB_TYPE  = sqlite3
HOST     = localhost:3306
NAME     = gitea
USER     = root
PASSWD   =
SCHEMA   =
SSL_MODE = disable
CHARSET  = utf8

[indexer]
ISSUE_INDEXER_PATH = /data/gitea/indexers/issues.bleve

[session]
PROVIDER_CONFIG = /data/gitea/sessions
PROVIDER        = file

[picture]
AVATAR_UPLOAD_PATH            = /data/gitea/avatars
REPOSITORY_AVATAR_UPLOAD_PATH = /data/gitea/repo-avatars
DISABLE_GRAVATAR              = false
ENABLE_FEDERATED_AVATAR       = true

[attachment]
PATH = /data/gitea/attachments

[log]
ROOT_PATH = /data/gitea/log
MODE      = file
LEVEL     = info

[security]
INSTALL_LOCK   = true
SECRET_KEY     = SECRET
INTERNAL_TOKEN = TOKEN

[service]
DISABLE_REGISTRATION              = true
REQUIRE_SIGNIN_VIEW               = false
REGISTER_EMAIL_CONFIRM            = false
ENABLE_NOTIFY_MAIL                = true
ALLOW_ONLY_EXTERNAL_REGISTRATION  = false
ENABLE_CAPTCHA                    = true
DEFAULT_KEEP_EMAIL_PRIVATE        = true
DEFAULT_ALLOW_CREATE_ORGANIZATION = true
DEFAULT_ENABLE_TIMETRACKING       = true
NO_REPLY_ADDRESS                  = HOST_NAME

[oauth2]
JWT_SECRET = SECRET

[mailer]
ENABLED = true
HOST    = smtp.gmail.com:465
FROM    = EMAIL@gmail.com
USER    = EMAIL@gmail.com
PASSWD  = PWD

[openid]
ENABLE_OPENID_SIGNIN = true
ENABLE_OPENID_SIGNUP = false
```
