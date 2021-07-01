# sqlc 扩展，仅用来编译表结构体

```
git clone -b main-ex github.com/ymzuiku/sqlc
```

确保本地有 go 环境, 编译 sqlm 全局执行程序

```bash
go install ./cmd/sqlm
```

在项目中创建 sqlc.yaml：

```yaml
# bash run: sqlm generate
version: "1"
packages:
  - name: "models"
    path: "./models"
    schema: "./migrations/"
    engine: "postgresql"
    emit_prepared_queries: false
    emit_interface: false
    emit_exact_table_names: false
    emit_empty_slices: false
    emit_json_tags: true
    json_tags_case_style: "camel"
overrides:
  - go_type: "github.com/gofrs/uuid.UUID"
    db_type: "uuid"
```

进入项目根目录，确保项目中 migrations 中有迁移文件，编译：

```bash
sqlm generate
```

## 自定义标签

sqlc is very perfect database model generation tool, we use sqlc and gorm(use dynamic query). This pull request is extends use sql comment custom go struct tags it's style:

Schema example code in comment:

```
@<tagName>:<tagValue>
```

Examples: Add comment in SQL(Postgres):

```sql
COMMENT ON COLUMN account.id is '@gorm:primaryKey @validate:required,min=3,max=32';
```

Generate go struct code:

```
type Account struct {
  ID  int32  `gorm:"primaryKey" json:"id" validate:"required,min=3,max=32"`
}
```

# sqlc: A SQL Compiler

![go](https://github.com/kyleconroy/sqlc/workflows/go/badge.svg) [![Go Report Card](https://goreportcard.com/badge/github.com/kyleconroy/sqlc)](https://goreportcard.com/report/github.com/kyleconroy/sqlc)

sqlc generates **type-safe code** from SQL. Here's how it works:

1. You write queries in SQL.
1. You run sqlc to generate code with type-safe interfaces to those queries.
1. You write application code that calls the generated code.

Check out [an interactive example](https://play.sqlc.dev/) to see it in action.

## Overview

- [Documentation](https://docs.sqlc.dev)
- [Installation](https://docs.sqlc.dev/en/latest/overview/install.html)
- [Playground](https://play.sqlc.dev)
- [Website](https://sqlc.dev)

## Sponsors

sqlc development is funded by our [generous sponsors](https://github.com/sponsors/kyleconroy), including the following companies:

- [Meter](https://meter.com)
- [ngrok](https://ngrok.com)

If you use sqlc at your company, please consider [becoming a sponsor](https://github.com/sponsors/kyleconroy) today.

Sponsors receive priority support via the sqlc Slack organization.

## Acknowledgements

sqlc was inspired by [PugSQL](https://pugsql.org/) and [HugSQL](https://www.hugsql.org/).
