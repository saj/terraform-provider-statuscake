---
layout: "statuscake"
page_title: "StatusCake: statuscake_ssl"
sidebar_current: "docs-statuscake-ssl"
description: |-
  The statuscake_ssl resource allows StatusCake ssl tests to be managed by Terraform.
---

# statuscake\_ssl

The ssl resource allows StatusCake ssl tests to be managed by Terraform.

## Example Usage

```hcl
resource "statuscake_ssl" "google" {
  domain         = "https://www.google.com"
  contact_group  = ["3", "12345"]
  check_rate     = 3600
  alert_at       = "3,14,30"
  alert_reminder = true
  alert_expiry   = true
  alert_broken   = false
  alert_mixed    = true
}
```

## Argument Reference

The following arguments are supported:

* `domain` - (Required) URL to check, has to start with https://
* `contact_group` - (Optional) Set test contact groups, must be array of strings.
* `check_rate` - (Optional) Test check rate in seconds. Defaults to 86400. May be set to one of 600, 1800, 3600, 86400, or 2073600.
* `alert_at` - (Required) Reminder alerting intervals. This string value must be specified as exactly three comma-separated positive integers. Each integer is a relative measure in days. For example, the string `"3,14,30"` will trigger an initial reminder alert at thirty days prior to certificate expiration, a second reminder at fourteen days, then -- if the certificate is still yet to be renewed -- a final reminder three days prior to certificate expiration.
* `alert_reminder` - (Required) Set to true to enable expiration reminder alerts. False to disable. Alerts are sent prior to certificate expiration at intervals defined by `alert_at`.
* `alert_expiry` - (Required) Set to true to enable expiration alerts. False to disable
* `alert_broken` - (Required) Set to true to enable broken alerts. False to disable
* `alert_mixed` - (Required) Set to true to enable mixed content alerts. False to disable

## Attributes Reference

The following attribute is exported:

* `ssl_id` - A unique identifier for the ssl test.
* `issuer_cn` - 
* `paused` - Whether the test has been paused (Administrative only)
* `cert_score` - Certificate score in %
* `cipher_score` - Cipher strength in %
* `cert_status` - Certificate status
* `cipher` - Cipher code (SSL spec)
* `valid_from_utc` - Certificate Validity Start (In UTC/GMT+0)
* `valid_until_utc` - Certificate Validity End (In UTC/GMT+0)
* `mixed_content` - Mixed content if present. Empty array if not.
* `last_reminder` - The last reminder to be detected (days)
* `last_updated_utc` - When the certificate has last been updated (Either by user action or by testing)
* `flags` :
    * `is_extended` : Certificate has an Extended Validation certificate
    * `has_pfs` : Certificate has Perfect Forward Secrecy enabled
    * `is_broken` : Certificate has errors
    * `is_expired` : Certificate is expired
    * `is_missing` : Certificate not present
    * `is_revoked` : Certificate has been revoked by CA
    * `is_mixed` : Website contains Mixed Content

## Import

StatusCake ssl tests can be imported using the ssl id, e.g.

```
tf import statuscake_ssl.example 123
```
