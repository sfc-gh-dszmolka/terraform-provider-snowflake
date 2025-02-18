---
# generated by https://github.com/hashicorp/terraform-plugin-docs
page_title: "snowflake_table_grant Resource - terraform-provider-snowflake"
subcategory: ""
description: |-
  
---

# snowflake_table_grant (Resource)



## Example Usage

```terraform
resource "snowflake_table_grant" "grant" {
  database_name = "database"
  schema_name   = "schema"
  table_name    = "table"

  privilege = "SELECT"
  roles     = ["role1"]
  shares    = ["share1"]

  on_future         = false
  with_grant_option = false
}
```

<!-- schema generated by tfplugindocs -->
## Schema

### Required

- `database_name` (String) The name of the database containing the current or future tables on which to grant privileges.

### Optional

- `enable_multiple_grants` (Boolean) When this is set to true, multiple grants of the same type can be created. This will cause Terraform to not revoke grants applied to roles and objects outside Terraform.
- `on_all` (Boolean) When this is set to true and a schema_name is provided, apply this grant on all tables in the given schema. When this is true and no schema_name is provided apply this grant on all tables in the given database. The table_name and shares fields must be unset in order to use on_all. Cannot be used together with on_future.
- `on_future` (Boolean) When this is set to true and a schema_name is provided, apply this grant on all future tables in the given schema. When this is true and no schema_name is provided apply this grant on all future tables in the given database. The table_name and shares fields must be unset in order to use on_future. Cannot be used together with on_all.
- `privilege` (String) The privilege to grant on the current or future table.
- `roles` (Set of String) Grants privilege to these roles.
- `schema_name` (String) The name of the schema containing the current or future tables on which to grant privileges.
- `shares` (Set of String) Grants privilege to these shares (only valid if on_future or on_all are unset).
- `table_name` (String) The name of the table on which to grant privileges immediately (only valid if on_future or on_all are unset).
- `with_grant_option` (Boolean) When this is set to true, allows the recipient role to grant the privileges to other roles.

### Read-Only

- `id` (String) The ID of this resource.

## Import

Import is supported using the following syntax:

```shell
# format is database_name|schema_name|table_name|privilege|with_grant_option|on_future|on_all|roles|shares
terraform import snowflake_table_grant.example "MY_DATABASE|MY_SCHEMA|MY_TABLE|USAGE|false|false|false|role1,role2|share1,share2"
```
