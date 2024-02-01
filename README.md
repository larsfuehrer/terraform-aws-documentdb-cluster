
<!-- markdownlint-disable -->
# terraform-aws-documentdb-cluster<a href="https://cpco.io/homepage"><img align="right" src="https://cloudposse.com/logo-300x69.svg" width="150" /></a> [![Latest Release](https://img.shields.io/github/release/cloudposse/terraform-aws-documentdb-cluster.svg)](https://github.com/cloudposse/terraform-aws-documentdb-cluster/releases/latest) [![Slack Community](https://slack.cloudposse.com/badge.svg)](https://slack.cloudposse.com)
<!-- markdownlint-restore -->


<!--




  ** DO NOT EDIT THIS FILE
  **
  ** This file was automatically generated by the `build-harness`.
  ** 1) Make all changes to `README.yaml`
  ** 2) Run `make init` (you only need to do this once)
  ** 3) Run`make readme` to rebuild this file.
  **
  ** (We maintain HUNDREDS of open source projects. This is how we maintain our sanity.)
  **





-->

Terraform module to provision an [`Amazon DocumentDB`](https://aws.amazon.com/documentdb/) cluster.


---
> [!NOTE]
> This project is part of Cloud Posse's comprehensive ["SweetOps"](https://cpco.io/sweetops) approach towards DevOps.
> <a href="https://cpco.io/terraform-modules"><img src="https://docs.cloudposse.com/images/terraform-open-source-modules.svg" align="right" /></a>
>
> It's 100% Open Source and licensed under the [APACHE2](LICENSE).
>
> We literally have [*hundreds of terraform modules*][terraform_modules] that are Open Source and well-maintained. Check them out!

[![README Header][readme_header_img]][readme_header_link]




## Usage



> **Important**
> We do not pin modules to versions in Cloud Posse's examples because of the
> difficulty of keeping the versions in the documentation in sync with the latest released versions.
> We highly recommend that in your code you pin the version to the exact version you are
> using so that your infrastructure remains stable, and update versions in a
> systematic way so that they do not catch you by surprise.




For a complete example, see [examples/complete](examples/complete).

For automated tests of the complete example using [bats](https://github.com/bats-core/bats-core) and [Terratest](https://github.com/gruntwork-io/terratest) (which tests and deploys the example on AWS), see [test](test).

```hcl
module "documentdb_cluster" {
  source = "cloudposse/documentdb-cluster/aws"
  # Cloud Posse recommends pinning every module to a specific version
  # version = "x.x.x"
  namespace               = "eg"
  stage                   = "testing"
  name                    = "docdb"
  cluster_size            = 3
  master_username         = "admin1"
  master_password         = "Test123456789"
  instance_class          = "db.r4.large"
  vpc_id                  = "vpc-xxxxxxxx"
  subnet_ids              = ["subnet-xxxxxxxx", "subnet-yyyyyyyy"]
  allowed_security_groups = ["sg-xxxxxxxx"]
  zone_id                 = "Zxxxxxxxx"
}
```






<!-- markdownlint-disable -->
## Makefile Targets
```text
Available targets:

  help                                Help screen
  help/all                            Display help for all targets
  help/short                          This help short screen
  lint                                Lint terraform code

```
<!-- markdownlint-restore -->
<!-- markdownlint-disable -->
## Requirements

| Name | Version |
|------|---------|
| <a name="requirement_terraform"></a> [terraform](#requirement\_terraform) | >= 0.14.0 |
| <a name="requirement_aws"></a> [aws](#requirement\_aws) | >= 2.0 |
| <a name="requirement_local"></a> [local](#requirement\_local) | >= 1.3 |
| <a name="requirement_random"></a> [random](#requirement\_random) | >= 1.0 |

## Providers

| Name | Version |
|------|---------|
| <a name="provider_aws"></a> [aws](#provider\_aws) | >= 2.0 |
| <a name="provider_random"></a> [random](#provider\_random) | >= 1.0 |

## Modules

| Name | Source | Version |
|------|--------|---------|
| <a name="module_dns_master"></a> [dns\_master](#module\_dns\_master) | cloudposse/route53-cluster-hostname/aws | 0.12.2 |
| <a name="module_dns_replicas"></a> [dns\_replicas](#module\_dns\_replicas) | cloudposse/route53-cluster-hostname/aws | 0.12.2 |
| <a name="module_this"></a> [this](#module\_this) | cloudposse/label/null | 0.25.0 |

## Resources

| Name | Type |
|------|------|
| [aws_docdb_cluster.default](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/docdb_cluster) | resource |
| [aws_docdb_cluster_instance.default](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/docdb_cluster_instance) | resource |
| [aws_docdb_cluster_parameter_group.default](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/docdb_cluster_parameter_group) | resource |
| [aws_docdb_subnet_group.default](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/docdb_subnet_group) | resource |
| [aws_security_group.default](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/security_group) | resource |
| [aws_security_group_rule.allow_ingress_from_self](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/security_group_rule) | resource |
| [aws_security_group_rule.egress](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/security_group_rule) | resource |
| [aws_security_group_rule.ingress_cidr_blocks](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/security_group_rule) | resource |
| [aws_security_group_rule.ingress_security_groups](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/security_group_rule) | resource |
| [random_password.password](https://registry.terraform.io/providers/hashicorp/random/latest/docs/resources/password) | resource |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| <a name="input_additional_tag_map"></a> [additional\_tag\_map](#input\_additional\_tag\_map) | Additional key-value pairs to add to each map in `tags_as_list_of_maps`. Not added to `tags` or `id`.<br>This is for some rare cases where resources want additional configuration of tags<br>and therefore take a list of maps with tag key, value, and additional configuration. | `map(string)` | `{}` | no |
| <a name="input_allow_ingress_from_self"></a> [allow\_ingress\_from\_self](#input\_allow\_ingress\_from\_self) | Adds the Document DB security group itself as a source for ingress rules. Useful when this security group will be shared with applications. | `bool` | `false` | no |
| <a name="input_allowed_cidr_blocks"></a> [allowed\_cidr\_blocks](#input\_allowed\_cidr\_blocks) | List of CIDR blocks to be allowed to connect to the DocumentDB cluster | `list(string)` | `[]` | no |
| <a name="input_allowed_security_groups"></a> [allowed\_security\_groups](#input\_allowed\_security\_groups) | List of existing Security Groups to be allowed to connect to the DocumentDB cluster | `list(string)` | `[]` | no |
| <a name="input_apply_immediately"></a> [apply\_immediately](#input\_apply\_immediately) | Specifies whether any cluster modifications are applied immediately, or during the next maintenance window | `bool` | `true` | no |
| <a name="input_attributes"></a> [attributes](#input\_attributes) | ID element. Additional attributes (e.g. `workers` or `cluster`) to add to `id`,<br>in the order they appear in the list. New attributes are appended to the<br>end of the list. The elements of the list are joined by the `delimiter`<br>and treated as a single ID element. | `list(string)` | `[]` | no |
| <a name="input_auto_minor_version_upgrade"></a> [auto\_minor\_version\_upgrade](#input\_auto\_minor\_version\_upgrade) | Specifies whether any minor engine upgrades will be applied automatically to the DB instance during the maintenance window or not | `bool` | `true` | no |
| <a name="input_cluster_dns_name"></a> [cluster\_dns\_name](#input\_cluster\_dns\_name) | Name of the cluster CNAME record to create in the parent DNS zone specified by `zone_id`. If left empty, the name will be auto-asigned using the format `master.var.name` | `string` | `""` | no |
| <a name="input_cluster_family"></a> [cluster\_family](#input\_cluster\_family) | The family of the DocumentDB cluster parameter group. For more details, see https://docs.aws.amazon.com/documentdb/latest/developerguide/db-cluster-parameter-group-create.html | `string` | `"docdb3.6"` | no |
| <a name="input_cluster_parameters"></a> [cluster\_parameters](#input\_cluster\_parameters) | List of DB parameters to apply | <pre>list(object({<br>    apply_method = string<br>    name         = string<br>    value        = string<br>  }))</pre> | `[]` | no |
| <a name="input_cluster_size"></a> [cluster\_size](#input\_cluster\_size) | Number of DB instances to create in the cluster | `number` | `3` | no |
| <a name="input_context"></a> [context](#input\_context) | Single object for setting entire context at once.<br>See description of individual variables for details.<br>Leave string and numeric variables as `null` to use default value.<br>Individual variable settings (non-null) override settings in context object,<br>except for attributes, tags, and additional\_tag\_map, which are merged. | `any` | <pre>{<br>  "additional_tag_map": {},<br>  "attributes": [],<br>  "delimiter": null,<br>  "descriptor_formats": {},<br>  "enabled": true,<br>  "environment": null,<br>  "id_length_limit": null,<br>  "label_key_case": null,<br>  "label_order": [],<br>  "label_value_case": null,<br>  "labels_as_tags": [<br>    "unset"<br>  ],<br>  "name": null,<br>  "namespace": null,<br>  "regex_replace_chars": null,<br>  "stage": null,<br>  "tags": {},<br>  "tenant": null<br>}</pre> | no |
| <a name="input_db_port"></a> [db\_port](#input\_db\_port) | DocumentDB port | `number` | `27017` | no |
| <a name="input_deletion_protection"></a> [deletion\_protection](#input\_deletion\_protection) | A value that indicates whether the DB cluster has deletion protection enabled | `bool` | `false` | no |
| <a name="input_delimiter"></a> [delimiter](#input\_delimiter) | Delimiter to be used between ID elements.<br>Defaults to `-` (hyphen). Set to `""` to use no delimiter at all. | `string` | `null` | no |
| <a name="input_descriptor_formats"></a> [descriptor\_formats](#input\_descriptor\_formats) | Describe additional descriptors to be output in the `descriptors` output map.<br>Map of maps. Keys are names of descriptors. Values are maps of the form<br>`{<br>   format = string<br>   labels = list(string)<br>}`<br>(Type is `any` so the map values can later be enhanced to provide additional options.)<br>`format` is a Terraform format string to be passed to the `format()` function.<br>`labels` is a list of labels, in order, to pass to `format()` function.<br>Label values will be normalized before being passed to `format()` so they will be<br>identical to how they appear in `id`.<br>Default is `{}` (`descriptors` output will be empty). | `any` | `{}` | no |
| <a name="input_enable_performance_insights"></a> [enable\_performance\_insights](#input\_enable\_performance\_insights) | Specifies whether to enable Performance Insights for the DB Instance. | `bool` | `false` | no |
| <a name="input_enabled"></a> [enabled](#input\_enabled) | Set to false to prevent the module from creating any resources | `bool` | `null` | no |
| <a name="input_enabled_cloudwatch_logs_exports"></a> [enabled\_cloudwatch\_logs\_exports](#input\_enabled\_cloudwatch\_logs\_exports) | List of log types to export to cloudwatch. The following log types are supported: `audit`, `error`, `general`, `slowquery` | `list(string)` | `[]` | no |
| <a name="input_engine"></a> [engine](#input\_engine) | The name of the database engine to be used for this DB cluster. Defaults to `docdb`. Valid values: `docdb` | `string` | `"docdb"` | no |
| <a name="input_engine_version"></a> [engine\_version](#input\_engine\_version) | The version number of the database engine to use | `string` | `"3.6.0"` | no |
| <a name="input_environment"></a> [environment](#input\_environment) | ID element. Usually used for region e.g. 'uw2', 'us-west-2', OR role 'prod', 'staging', 'dev', 'UAT' | `string` | `null` | no |
| <a name="input_id_length_limit"></a> [id\_length\_limit](#input\_id\_length\_limit) | Limit `id` to this many characters (minimum 6).<br>Set to `0` for unlimited length.<br>Set to `null` for keep the existing setting, which defaults to `0`.<br>Does not affect `id_full`. | `number` | `null` | no |
| <a name="input_instance_class"></a> [instance\_class](#input\_instance\_class) | The instance class to use. For more details, see https://docs.aws.amazon.com/documentdb/latest/developerguide/db-instance-classes.html#db-instance-class-specs | `string` | `"db.r4.large"` | no |
| <a name="input_kms_key_id"></a> [kms\_key\_id](#input\_kms\_key\_id) | The ARN for the KMS encryption key. When specifying `kms_key_id`, `storage_encrypted` needs to be set to `true` | `string` | `""` | no |
| <a name="input_label_key_case"></a> [label\_key\_case](#input\_label\_key\_case) | Controls the letter case of the `tags` keys (label names) for tags generated by this module.<br>Does not affect keys of tags passed in via the `tags` input.<br>Possible values: `lower`, `title`, `upper`.<br>Default value: `title`. | `string` | `null` | no |
| <a name="input_label_order"></a> [label\_order](#input\_label\_order) | The order in which the labels (ID elements) appear in the `id`.<br>Defaults to ["namespace", "environment", "stage", "name", "attributes"].<br>You can omit any of the 6 labels ("tenant" is the 6th), but at least one must be present. | `list(string)` | `null` | no |
| <a name="input_label_value_case"></a> [label\_value\_case](#input\_label\_value\_case) | Controls the letter case of ID elements (labels) as included in `id`,<br>set as tag values, and output by this module individually.<br>Does not affect values of tags passed in via the `tags` input.<br>Possible values: `lower`, `title`, `upper` and `none` (no transformation).<br>Set this to `title` and set `delimiter` to `""` to yield Pascal Case IDs.<br>Default value: `lower`. | `string` | `null` | no |
| <a name="input_labels_as_tags"></a> [labels\_as\_tags](#input\_labels\_as\_tags) | Set of labels (ID elements) to include as tags in the `tags` output.<br>Default is to include all labels.<br>Tags with empty values will not be included in the `tags` output.<br>Set to `[]` to suppress all generated tags.<br>**Notes:**<br>  The value of the `name` tag, if included, will be the `id`, not the `name`.<br>  Unlike other `null-label` inputs, the initial setting of `labels_as_tags` cannot be<br>  changed in later chained modules. Attempts to change it will be silently ignored. | `set(string)` | <pre>[<br>  "default"<br>]</pre> | no |
| <a name="input_master_password"></a> [master\_password](#input\_master\_password) | (Required unless a snapshot\_identifier is provided) Password for the master DB user. Note that this may show up in logs, and it will be stored in the state file. Please refer to the DocumentDB Naming Constraints | `string` | `""` | no |
| <a name="input_master_username"></a> [master\_username](#input\_master\_username) | (Required unless a snapshot\_identifier is provided) Username for the master DB user | `string` | `"admin1"` | no |
| <a name="input_name"></a> [name](#input\_name) | ID element. Usually the component or solution name, e.g. 'app' or 'jenkins'.<br>This is the only ID element not also included as a `tag`.<br>The "name" tag is set to the full `id` string. There is no tag with the value of the `name` input. | `string` | `null` | no |
| <a name="input_namespace"></a> [namespace](#input\_namespace) | ID element. Usually an abbreviation of your organization name, e.g. 'eg' or 'cp', to help ensure generated IDs are globally unique | `string` | `null` | no |
| <a name="input_preferred_backup_window"></a> [preferred\_backup\_window](#input\_preferred\_backup\_window) | Daily time range during which the backups happen | `string` | `"07:00-09:00"` | no |
| <a name="input_preferred_maintenance_window"></a> [preferred\_maintenance\_window](#input\_preferred\_maintenance\_window) | The window to perform maintenance in. Syntax: `ddd:hh24:mi-ddd:hh24:mi`. | `string` | `"Mon:22:00-Mon:23:00"` | no |
| <a name="input_reader_dns_name"></a> [reader\_dns\_name](#input\_reader\_dns\_name) | Name of the reader endpoint CNAME record to create in the parent DNS zone specified by `zone_id`. If left empty, the name will be auto-asigned using the format `replicas.var.name` | `string` | `""` | no |
| <a name="input_regex_replace_chars"></a> [regex\_replace\_chars](#input\_regex\_replace\_chars) | Terraform regular expression (regex) string.<br>Characters matching the regex will be removed from the ID elements.<br>If not set, `"/[^a-zA-Z0-9-]/"` is used to remove all characters other than hyphens, letters and digits. | `string` | `null` | no |
| <a name="input_retention_period"></a> [retention\_period](#input\_retention\_period) | Number of days to retain backups for | `number` | `5` | no |
| <a name="input_skip_final_snapshot"></a> [skip\_final\_snapshot](#input\_skip\_final\_snapshot) | Determines whether a final DB snapshot is created before the DB cluster is deleted | `bool` | `true` | no |
| <a name="input_snapshot_identifier"></a> [snapshot\_identifier](#input\_snapshot\_identifier) | Specifies whether or not to create this cluster from a snapshot. You can use either the name or ARN when specifying a DB cluster snapshot, or the ARN when specifying a DB snapshot | `string` | `""` | no |
| <a name="input_stage"></a> [stage](#input\_stage) | ID element. Usually used to indicate role, e.g. 'prod', 'staging', 'source', 'build', 'test', 'deploy', 'release' | `string` | `null` | no |
| <a name="input_storage_encrypted"></a> [storage\_encrypted](#input\_storage\_encrypted) | Specifies whether the DB cluster is encrypted | `bool` | `true` | no |
| <a name="input_storage_type"></a> [storage\_type](#input\_storage\_type) | The storage type to associate with the DB cluster. Valid values: standard, iopt1 | `string` | `"standard"` | no |
| <a name="input_subnet_ids"></a> [subnet\_ids](#input\_subnet\_ids) | List of VPC subnet IDs to place DocumentDB instances in | `list(string)` | n/a | yes |
| <a name="input_tags"></a> [tags](#input\_tags) | Additional tags (e.g. `{'BusinessUnit': 'XYZ'}`).<br>Neither the tag keys nor the tag values will be modified by this module. | `map(string)` | `{}` | no |
| <a name="input_tenant"></a> [tenant](#input\_tenant) | ID element \_(Rarely used, not included by default)\_. A customer identifier, indicating who this instance of a resource is for | `string` | `null` | no |
| <a name="input_vpc_id"></a> [vpc\_id](#input\_vpc\_id) | VPC ID to create the cluster in (e.g. `vpc-a22222ee`) | `string` | n/a | yes |
| <a name="input_zone_id"></a> [zone\_id](#input\_zone\_id) | Route53 parent zone ID. If provided (not empty), the module will create sub-domain DNS records for the DocumentDB master and replicas | `string` | `""` | no |

## Outputs

| Name | Description |
|------|-------------|
| <a name="output_arn"></a> [arn](#output\_arn) | Amazon Resource Name (ARN) of the cluster |
| <a name="output_cluster_name"></a> [cluster\_name](#output\_cluster\_name) | Cluster Identifier |
| <a name="output_endpoint"></a> [endpoint](#output\_endpoint) | Endpoint of the DocumentDB cluster |
| <a name="output_instance_name"></a> [instance\_name](#output\_instance\_name) | Cluster Instance Identifier |
| <a name="output_master_host"></a> [master\_host](#output\_master\_host) | DB master hostname |
| <a name="output_master_password"></a> [master\_password](#output\_master\_password) | Password for the master DB user |
| <a name="output_master_username"></a> [master\_username](#output\_master\_username) | Username for the master DB user |
| <a name="output_reader_endpoint"></a> [reader\_endpoint](#output\_reader\_endpoint) | A read-only endpoint of the DocumentDB cluster, automatically load-balanced across replicas |
| <a name="output_replicas_host"></a> [replicas\_host](#output\_replicas\_host) | DB replicas hostname |
| <a name="output_security_group_arn"></a> [security\_group\_arn](#output\_security\_group\_arn) | ARN of the DocumentDB cluster Security Group |
| <a name="output_security_group_id"></a> [security\_group\_id](#output\_security\_group\_id) | ID of the DocumentDB cluster Security Group |
| <a name="output_security_group_name"></a> [security\_group\_name](#output\_security\_group\_name) | Name of the DocumentDB cluster Security Group |
<!-- markdownlint-restore -->


## Related Projects

Check out these related projects.

- [terraform-aws-rds](https://github.com/cloudposse/terraform-aws-rds) - Terraform module to provision AWS RDS instances for MySQL or Postgres
- [terraform-aws-rds-cluster](https://github.com/cloudposse/terraform-aws-rds-cluster) - Terraform module to provision an RDS Aurora cluster for MySQL or Postgres
- [terraform-aws-rds-cloudwatch-sns-alarms](https://github.com/cloudposse/terraform-aws-rds-cloudwatch-sns-alarms) - Terraform module that configures important RDS alerts using CloudWatch and sends them to an SNS topic


## References

For additional context, refer to some of these links.

- [Creating an Amazon DocumentDB Cluster](https://docs.aws.amazon.com/documentdb/latest/developerguide/db-cluster-create.html) - official AWS documentation on how to create a DocumentDB cluster
- [Amazon DocumentDB Instance Class Specifications](https://docs.aws.amazon.com/documentdb/latest/developerguide/db-instance-classes.html#db-instance-class-specs) - provides details of the Amazon DocumentDB instance classes
- [Creating an Amazon DocumentDB Cluster Parameter Group](https://docs.aws.amazon.com/documentdb/latest/developerguide/db-cluster-parameter-group-create.html) - official AWS documentation on how to create an Amazon DocumentDB Cluster Parameter Group
- [Amazon DocumentDB Limits](https://docs.aws.amazon.com/documentdb/latest/developerguide/limits.html) - describes the resource limits and naming constraints for Amazon DocumentDB
- [Understanding Amazon DocumentDB Amazon Resource Names (ARNs)](https://docs.aws.amazon.com/documentdb/latest/developerguide/documentdb-arns.html) - describes ARN formats for DocumentDB resources
- [Amazon DocumentDB Parameters](https://docs.aws.amazon.com/documentdb/latest/developerguide/db-cluster-parameters.html) - lists all the parameters that are specific to a DocumentDB cluster
- [Tagging Amazon DocumentDB Resources](https://docs.aws.amazon.com/documentdb/latest/developerguide/tagging.html) - describes how to use tags to add metadata to DocumentDB resources
- [Amazon DocumentDB FAQs](https://aws.amazon.com/documentdb/faqs/) - DocumentDB frequently asked questions
- [Troubleshooting Amazon DocumentDB](https://docs.aws.amazon.com/documentdb/latest/developerguide/troubleshooting.html) - provides information about how to troubleshoot problems that you might encounter when using Amazon DocumentDB


## ✨ Contributing

This project is under active development, and we encourage contributions from our community.
Many thanks to our outstanding contributors:

<a href="https://github.com/cloudposse/terraform-aws-documentdb-cluster/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=cloudposse/terraform-aws-documentdb-cluster&max=24" />
</a>

### 🐛 Bug Reports & Feature Requests

Please use the [issue tracker](https://github.com/cloudposse/terraform-aws-documentdb-cluster/issues) to report any bugs or file feature requests.

### 💻 Developing

If you are interested in being a contributor and want to get involved in developing this project or [help out](https://cpco.io/help-out) with Cloud Posse's other projects, we would love to hear from you! Shoot us an [email][email].

In general, PRs are welcome. We follow the typical "fork-and-pull" Git workflow.

1. **Fork** the repo on GitHub
2. **Clone** the project to your own machine
3. **Commit** changes to your own branch
4. **Push** your work back up to your fork
5. Submit a **Pull Request** so that we can review your changes

**NOTE:** Be sure to merge the latest changes from "upstream" before making a pull request!

### 🌎 Slack Community

Join our [Open Source Community][slack] on Slack. It's **FREE** for everyone! Our "SweetOps" community is where you get to talk with others who share a similar vision for how to rollout and manage infrastructure. This is the best place to talk shop, ask questions, solicit feedback, and work together as a community to build totally *sweet* infrastructure.

### 📰 Newsletter

Sign up for [our newsletter][newsletter] that covers everything on our technology radar.  Receive updates on what we're up to on GitHub as well as awesome new projects we discover.

### 📆 Office Hours <img src="https://img.cloudposse.com/fit-in/200x200/https://cloudposse.com/wp-content/uploads/2019/08/Powered-by-Zoom.png" align="right" />

[Join us every Wednesday via Zoom][office_hours] for our weekly "Lunch & Learn" sessions. It's **FREE** for everyone!

## About

This project is maintained and funded by [Cloud Posse, LLC][website].
<a href="https://cpco.io/homepage"><img src="https://cloudposse.com/logo-300x69.svg" align="right" /></a>

We are a [**DevOps Accelerator**][commercial_support]. We'll help you build your cloud infrastructure from the ground up so you can own it. Then we'll show you how to operate it and stick around for as long as you need us.

[![Learn More](https://img.shields.io/badge/learn%20more-success.svg?style=for-the-badge)][commercial_support]

Work directly with our team of DevOps experts via email, slack, and video conferencing.

We deliver 10x the value for a fraction of the cost of a full-time engineer. Our track record is not even funny. If you want things done right and you need it done FAST, then we're your best bet.

- **Reference Architecture.** You'll get everything you need from the ground up built using 100% infrastructure as code.
- **Release Engineering.** You'll have end-to-end CI/CD with unlimited staging environments.
- **Site Reliability Engineering.** You'll have total visibility into your apps and microservices.
- **Security Baseline.** You'll have built-in governance with accountability and audit logs for all changes.
- **GitOps.** You'll be able to operate your infrastructure via Pull Requests.
- **Training.** You'll receive hands-on training so your team can operate what we build.
- **Questions.** You'll have a direct line of communication between our teams via a Shared Slack channel.
- **Troubleshooting.** You'll get help to triage when things aren't working.
- **Code Reviews.** You'll receive constructive feedback on Pull Requests.
- **Bug Fixes.** We'll rapidly work with you to fix any bugs in our projects.

[![README Commercial Support][readme_commercial_support_img]][readme_commercial_support_link]
## License

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

See [LICENSE](LICENSE) for full details.

```text
Licensed to the Apache Software Foundation (ASF) under one
or more contributor license agreements.  See the NOTICE file
distributed with this work for additional information
regarding copyright ownership.  The ASF licenses this file
to you under the Apache License, Version 2.0 (the
"License"); you may not use this file except in compliance
with the License.  You may obtain a copy of the License at

  https://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing,
software distributed under the License is distributed on an
"AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
KIND, either express or implied.  See the License for the
specific language governing permissions and limitations
under the License.
```

## Trademarks

All other trademarks referenced herein are the property of their respective owners.
---
Copyright © 2017-2024 [Cloud Posse, LLC](https://cpco.io/copyright)
[![README Footer][readme_footer_img]][readme_footer_link]
[![Beacon][beacon]][website]
<!-- markdownlint-disable -->
[logo]: https://cloudposse.com/logo-300x69.svg
[docs]: https://cpco.io/docs?utm_source=github&utm_medium=readme&utm_campaign=cloudposse/terraform-aws-documentdb-cluster&utm_content=docs
[website]: https://cpco.io/homepage?utm_source=github&utm_medium=readme&utm_campaign=cloudposse/terraform-aws-documentdb-cluster&utm_content=website
[github]: https://cpco.io/github?utm_source=github&utm_medium=readme&utm_campaign=cloudposse/terraform-aws-documentdb-cluster&utm_content=github
[jobs]: https://cpco.io/jobs?utm_source=github&utm_medium=readme&utm_campaign=cloudposse/terraform-aws-documentdb-cluster&utm_content=jobs
[hire]: https://cpco.io/hire?utm_source=github&utm_medium=readme&utm_campaign=cloudposse/terraform-aws-documentdb-cluster&utm_content=hire
[slack]: https://cpco.io/slack?utm_source=github&utm_medium=readme&utm_campaign=cloudposse/terraform-aws-documentdb-cluster&utm_content=slack
[twitter]: https://cpco.io/twitter?utm_source=github&utm_medium=readme&utm_campaign=cloudposse/terraform-aws-documentdb-cluster&utm_content=twitter
[office_hours]: https://cloudposse.com/office-hours?utm_source=github&utm_medium=readme&utm_campaign=cloudposse/terraform-aws-documentdb-cluster&utm_content=office_hours
[newsletter]: https://cpco.io/newsletter?utm_source=github&utm_medium=readme&utm_campaign=cloudposse/terraform-aws-documentdb-cluster&utm_content=newsletter
[email]: https://cpco.io/email?utm_source=github&utm_medium=readme&utm_campaign=cloudposse/terraform-aws-documentdb-cluster&utm_content=email
[commercial_support]: https://cpco.io/commercial-support?utm_source=github&utm_medium=readme&utm_campaign=cloudposse/terraform-aws-documentdb-cluster&utm_content=commercial_support
[we_love_open_source]: https://cpco.io/we-love-open-source?utm_source=github&utm_medium=readme&utm_campaign=cloudposse/terraform-aws-documentdb-cluster&utm_content=we_love_open_source
[terraform_modules]: https://cpco.io/terraform-modules?utm_source=github&utm_medium=readme&utm_campaign=cloudposse/terraform-aws-documentdb-cluster&utm_content=terraform_modules
[readme_header_img]: https://cloudposse.com/readme/header/img
[readme_header_link]: https://cloudposse.com/readme/header/link?utm_source=github&utm_medium=readme&utm_campaign=cloudposse/terraform-aws-documentdb-cluster&utm_content=readme_header_link
[readme_footer_img]: https://cloudposse.com/readme/footer/img
[readme_footer_link]: https://cloudposse.com/readme/footer/link?utm_source=github&utm_medium=readme&utm_campaign=cloudposse/terraform-aws-documentdb-cluster&utm_content=readme_footer_link
[readme_commercial_support_img]: https://cloudposse.com/readme/commercial-support/img
[readme_commercial_support_link]: https://cloudposse.com/readme/commercial-support/link?utm_source=github&utm_medium=readme&utm_campaign=cloudposse/terraform-aws-documentdb-cluster&utm_content=readme_commercial_support_link
[beacon]: https://ga-beacon.cloudposse.com/UA-76589703-4/cloudposse/terraform-aws-documentdb-cluster?pixel&cs=github&cm=readme&an=terraform-aws-documentdb-cluster
<!-- markdownlint-restore -->