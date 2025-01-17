---
subcategory: "Cloud (Stackdriver) Logging"
page_title: "Google: google_logging_organization_exclusion"
description: |-
  Manages a organization-level logging exclusion.
---

# google\_logging\_organization\_exclusion

Manages an organization-level logging exclusion. For more information see:

* [API documentation](https://cloud.google.com/logging/docs/reference/v2/rest/v2/organizations.exclusions)
* How-to Guides
    * [Excluding Logs](https://cloud.google.com/logging/docs/exclusions)

~> You can specify exclusions for log sinks created by terraform by using the exclusions field of `google_logging_organization_sink`

## Example Usage

```hcl
resource "google_logging_organization_exclusion" "my-exclusion" {
  name   = "my-instance-debug-exclusion"
  org_id = "123456789"

  description = "Exclude GCE instance debug logs"

  # Exclude all DEBUG or lower severity messages relating to instances
  filter = "resource.type = gce_instance AND severity <= DEBUG"
}
```

## Argument Reference

The following arguments are supported:

* `name` - (Required) The name of the logging exclusion.

* `org_id` - (Required) The organization to create the exclusion in.

* `description` - (Optional) A human-readable description.

* `disabled` - (Optional) Whether this exclusion rule should be disabled or not. This defaults to
    false.

* `filter` - (Required) The filter to apply when excluding logs. Only log entries that match the filter are excluded.
    See [Advanced Log Filters](https://cloud.google.com/logging/docs/view/advanced-filters) for information on how to
    write a filter.

## Attributes Reference

In addition to the arguments listed above, the following computed attributes are exported:

* `id` - an identifier for the resource with format `organizations/{{organization}}/exclusions/{{name}}`

## Import

Organization-level logging exclusions can be imported using their URI, e.g.

```
$ terraform import google_logging_organization_exclusion.my_exclusion organizations/{{organization}}/exclusions/{{name}}
```
