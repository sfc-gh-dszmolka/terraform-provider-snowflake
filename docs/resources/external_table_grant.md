---
# generated by https://github.com/hashicorp/terraform-plugin-docs
page_title: "snowflake_external_table_grant Resource - terraform-provider-snowflake"
subcategory: ""
description: |-
  
---

# snowflake_external_table_grant (Resource)



## Example Usage

```terraform
resource "snowflake_external_table_grant" "grant" {
  database_name       = "database"
  schema_name         = "schema"
  external_table_name = "external_table"

  privilege = "SELECT"
  roles     = ["role1", "role2"]

  shares = ["share1", "share2"]

  on_future         = false
  with_grant_option = false
}
```

<!-- schema generated by tfplugindocs -->
## Schema

### Required

- `database_name` (String) The name of the database containing the current or future external tables on which to grant privileges.
- `roles` (Set of String) Grants privilege to these roles.

### Optional

- `enable_multiple_grants` (Boolean) When this is set to true, multiple grants of the same type can be created. This will cause Terraform to not revoke grants applied to roles and objects outside Terraform.
- `external_table_name` (String) The name of the external table on which to grant privileges immediately (only valid if on_future is false).
- `on_all` (Boolean) When this is set to true and a schema_name is provided, apply this grant on all external tables in the given schema. When this is true and no schema_name is provided apply this grant on all external tables in the given database. The external_table_name and shares fields must be unset in order to use on_all. Cannot be used together with on_future.
- `on_future` (Boolean) When this is set to true and a schema_name is provided, apply this grant on all future external tables in the given schema. When this is true and no schema_name is provided apply this grant on all future external tables in the given database. The external_table_name and shares fields must be unset in order to use on_future. Cannot be used together with on_all.
- `privilege` (String) The privilege to grant on the current or future external table.
- `schema_name` (String) The name of the schema containing the current or future external tables on which to grant privileges.
- `shares` (Set of String) Grants privilege to these shares (only valid if on_future is false).
- `with_grant_option` (Boolean) When this is set to true, allows the recipient role to grant the privileges to other roles.

### Read-Only

- `id` (String) The ID of this resource.

## Import

Import is supported using the following syntax:

```shell
# format is database|schema|external_table|privilege|with_grant_option|on_future|roles|shares
terraform import snowflake_external_table_grant.example "MY_DATABASE|MY_SCHEMA|MY_TABLE_NAME|SELECT|false|false|role1,role2|share1,share2"
```
