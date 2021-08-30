
## Mongodbatlas_alert_configuration
Use mongodb's provider `mongodbatlas_alert_configuration` resource

## Pre-requirements

* [Mongodb atlas account](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) 
* [Terraform cli](https://learn.hashicorp.com/tutorials/terraform/install-cli)


## How to use this repo

- Clone
- Run
- Cleanup

---

### Clone the repo

```
git clone https://github.com/viv-garot/54775-Create-a-mongodbatlas_alert_configuration
```

### Change directory

```
cd 54775-Create-a-mongodbatlas_alert_configuration
```

### Run

* Follow mongodb documentation to
    * Create a mongodb atlas [account](https://docs.atlas.mongodb.com/getting-started/) and setup a free cluster
    * Create a [programatic API access](https://docs.atlas.mongodb.com/tutorial/manage-programmatic-access/#manage-programmatic-access-to-a-project) into the created Atlas project


* Update the main.tf file line 19 `project_id = # update with"<YOUR-PROJECT-ID>"`. The Organisation ID is found under `Organization Settings` in the cloud.mongodb.com webpage

* Export to your environment the API public and private key created earlier under the atlas project

```
$  export MONGODB_ATLAS_PUBLIC_KEY="xxxx"
$  export MONGODB_ATLAS_PRIVATE_KEY="xxxx"
```

* Init:

```
terraform init
```

_sample_:

```
terraform init

Initializing the backend...

Initializing provider plugins...
- Reusing previous version of mongodb/mongodbatlas from the dependency lock file
- Installing mongodb/mongodbatlas v1.0.0...
- Installed mongodb/mongodbatlas v1.0.0 (signed by a HashiCorp partner, key ID 2A32ED1F3AD25ABF)

Partner and community providers are signed by their developers.
If you'd like to know more about provider signing, you can read about it here:
https://www.terraform.io/docs/cli/plugins/signing.html

Terraform has been successfully initialized!

You may now begin working with Terraform. Try running "terraform plan" to see
any changes that are required for your infrastructure. All Terraform commands
should now work.

If you ever set or change modules or backend configuration for Terraform,
rerun this command to reinitialize your working directory. If you forget, other
commands will detect it and remind you to do so if necessary.
```

* Apply:

```
terraform apply
```

_sample_:

```
terraform apply

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

  # mongodbatlas_alert_configuration.test will be created
  + resource "mongodbatlas_alert_configuration" "test" {
      + alert_configuration_id = (known after apply)
      + created                = (known after apply)
      + enabled                = true
      + event_type             = "OUTSIDE_METRIC_THRESHOLD"
      + id                     = (known after apply)
      + project_id             = "612c98d1138b934a45ecb75d"
      + updated                = (known after apply)

      + matcher {
          + field_name = "HOSTNAME_AND_PORT"
          + operator   = "EQUALS"
          + value      = "SECONDARY"
        }

      + metric_threshold_config {
          + metric_name = "ASSERT_REGULAR"
          + mode        = "AVERAGE"
          + operator    = "LESS_THAN"
          + threshold   = 99
          + units       = "RAW"
        }

      + notification {
          + delay_min     = 0
          + email_enabled = true
          + interval_min  = 5
          + roles         = [
              + "GROUP_CLUSTER_MANAGER",
            ]
          + sms_enabled   = false
          + type_name     = "GROUP"
        }
    }

Plan: 1 to add, 0 to change, 0 to destroy.

Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.

  Enter a value: yes

mongodbatlas_alert_configuration.test: Creating...
mongodbatlas_alert_configuration.test: Creation complete after 4s [id=aWQ=:NjEyY2IxZjMzZmNkZmE0ZTE4NGRiZjQy-cHJvamVjdF9pZA==:NjEyYzk4ZDExMzhiOTM0YTQ1ZWNiNzVk]

Apply complete! Resources: 1 added, 0 changed, 0 destroyed.
```

* Confirm the new alert has been created in Atlas web page (Project > Visit Project Settings > Alerts > Alerts Settings)

![image](https://user-images.githubusercontent.com/85481359/131325724-4ed1b236-ad03-4529-a31e-3808b82d2e0f.png)

![image](https://user-images.githubusercontent.com/85481359/131325874-cb7e51c7-7782-4a42-bea5-28f2fd9c63fe.png)



### Cleanup

```
terraform destroy
```

_sample_:

```
terraform destroy --auto-approve=true
mongodbatlas_alert_configuration.test: Refreshing state... [id=aWQ=:NjEyY2IxZjMzZmNkZmE0ZTE4NGRiZjQy-cHJvamVjdF9pZA==:NjEyYzk4ZDExMzhiOTM0YTQ1ZWNiNzVk]

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  - destroy

Terraform will perform the following actions:

  # mongodbatlas_alert_configuration.test will be destroyed
  - resource "mongodbatlas_alert_configuration" "test" {
      - alert_configuration_id = "612cb1f33fcdfa4e184dbf42" -> null
      - created                = "2021-08-30T10:24:51Z" -> null
      - enabled                = true -> null
      - event_type             = "OUTSIDE_METRIC_THRESHOLD" -> null
      - id                     = "aWQ=:NjEyY2IxZjMzZmNkZmE0ZTE4NGRiZjQy-cHJvamVjdF9pZA==:NjEyYzk4ZDExMzhiOTM0YTQ1ZWNiNzVk" -> null
      - project_id             = "612c98d1138b934a45ecb75d" -> null
      - updated                = "2021-08-30T10:24:51Z" -> null

      - matcher {
          - field_name = "HOSTNAME_AND_PORT" -> null
          - operator   = "EQUALS" -> null
          - value      = "SECONDARY" -> null
        }

      - metric_threshold_config {
          - metric_name = "ASSERT_REGULAR" -> null
          - mode        = "AVERAGE" -> null
          - operator    = "LESS_THAN" -> null
          - threshold   = 99 -> null
          - units       = "RAW" -> null
        }

      - notification {
          - delay_min     = 0 -> null
          - email_enabled = true -> null
          - interval_min  = 5 -> null
          - roles         = [
              - "GROUP_CLUSTER_MANAGER",
            ] -> null
          - sms_enabled   = false -> null
          - type_name     = "GROUP" -> null
        }
    }

Plan: 0 to add, 0 to change, 1 to destroy.
mongodbatlas_alert_configuration.test: Destroying... [id=aWQ=:NjEyY2IxZjMzZmNkZmE0ZTE4NGRiZjQy-cHJvamVjdF9pZA==:NjEyYzk4ZDExMzhiOTM0YTQ1ZWNiNzVk]
mongodbatlas_alert_configuration.test: Destruction complete after 4s

Destroy complete! Resources: 1 destroyed.
```
