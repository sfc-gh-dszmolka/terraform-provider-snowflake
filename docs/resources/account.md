---
page_title: "snowflake_account Resource - terraform-provider-snowflake"
subcategory: ""
description: |-
  The account resource allows you to create and manage Snowflake accounts.
---

# snowflake_account (Resource)

The account resource allows you to create and manage Snowflake accounts.

    **WARNING** This resource cannot be destroyed!!! The only way to delete accounts is to go through [Snowflake Support](https://docs.snowflake.com/en/user-guide/organizations-manage-accounts.html#deleting-an-account)

    **NOTE** ORGADMIN priviliges are required for this resource

## Example Usage

```terraform
provider "snowflake" {
  role  = "ORGADMIN"
  alias = "orgadmin"
}

resource "snowflake_account" "ac1" {
  provider             = snowflake.orgadmin
  name                 = "SNOWFLAKE_TEST_ACCOUNT"
  admin_name           = "John Doe"
  admin_password       = "Abcd1234!"
  email                = "john.doe@snowflake.com"
  first_name           = "John"
  last_name            = "Doe"
  must_change_password = true
  edition              = "STANDARD"
  comment              = "Snowflake Test Account"
  region               = "AWS_US_WEST_2"
}
```

<!-- schema generated by tfplugindocs -->
## Schema

### Required

- `admin_name` (String) Login name of the initial administrative user of the account. A new user is created in the new account with this name and password and granted the ACCOUNTADMIN role in the account. A login name can be any string consisting of letters, numbers, and underscores. Login names are always case-insensitive.
- `edition` (String) [Snowflake Edition](https://docs.snowflake.com/en/user-guide/intro-editions.html) of the account. Valid values are: STANDARD | ENTERPRISE | BUSINESS_CRITICAL
- `email` (String, Sensitive) Email address of the initial administrative user of the account. This email address is used to send any notifications about the account.
- `name` (String) Specifies the identifier (i.e. name) for the account; must be unique within an organization, regardless of which Snowflake Region the account is in. In addition, the identifier must start with an alphabetic character and cannot contain spaces or special characters except for underscores (_). Note that if the account name includes underscores, features that do not accept account names with underscores (e.g. Okta SSO or SCIM) can reference a version of the account name that substitutes hyphens (-) for the underscores.

### Optional

- `admin_password` (String, Sensitive) Password for the initial administrative user of the account. Optional if the `ADMIN_RSA_PUBLIC_KEY` parameter is specified. For more information about passwords in Snowflake, see [Snowflake-provided Password Policy](https://docs.snowflake.com/en/sql-reference/sql/create-account.html#:~:text=Snowflake%2Dprovided%20Password%20Policy).
- `admin_rsa_public_key` (String, Sensitive) Assigns a public key to the initial administrative user of the account in order to implement [key pair authentication](https://docs.snowflake.com/en/sql-reference/sql/create-account.html#:~:text=key%20pair%20authentication) for the user. Optional if the `ADMIN_PASSWORD` parameter is specified.
- `comment` (String) Specifies a comment for the account.
- `first_name` (String, Sensitive) First name of the initial administrative user of the account
- `last_name` (String, Sensitive) Last name of the initial administrative user of the account
- `must_change_password` (Boolean) Specifies whether the new user created to administer the account is forced to change their password upon first login into the account.
- `region` (String) ID of the Snowflake Region where the account is created. If no value is provided, Snowflake creates the account in the same Snowflake Region as the current account (i.e. the account in which the CREATE ACCOUNT statement is executed.)
- `region_group` (String) ID of the Snowflake Region where the account is created. If no value is provided, Snowflake creates the account in the same Snowflake Region as the current account (i.e. the account in which the CREATE ACCOUNT statement is executed.)

### Read-Only

- `id` (String) The ID of this resource.
- `is_org_admin` (Boolean) Indicates whether the ORGADMIN role is enabled in an account. If TRUE, the role is enabled.

## Import

Import is supported using the following syntax:

```shell
terraform import snowflake_account.account <account_locator>
```
