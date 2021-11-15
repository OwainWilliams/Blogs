---
description: useful snippets
---

# SQL Statements



```
use <database_name>
go
EXEC sp_change_users_login 'Update_One', 'sde', 'sde'
go
```

`ALTER USER [LOGIN_NAME] WITH PASSWORD = 'PASSWORD'`

``

``

```
use <database_name>
go
ALTER USER sde WITH login = sde
go
```
