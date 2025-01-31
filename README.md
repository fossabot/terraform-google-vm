# terraform-google-vm
[![FOSSA Status](https://app.fossa.com/api/projects/git%2Bgithub.com%2Fboeyeb%2Fterraform-google-vm.svg?type=shield)](https://app.fossa.com/projects/git%2Bgithub.com%2Fboeyeb%2Fterraform-google-vm?ref=badge_shield)


This is a collection of opinionated submodules that can be used as building blocks to provision VMs in GCP:

* [Instance template](modules/instance_template)
* [Managed instance group](modules/mig)
* [Unmanaged instance group](modules/umig)

## Examples

Examples of how to use these modules can be found in the [examples](examples) folder.

## Project APIs

The following APIs must be enabled on your project:
- `compute.googleapis.com`
- `iam.googleapis.com`

See also the [project_services](modules/project_services) module (optional).

## Test Configuration

1. Create a `terraform.tfvars` file, using `terraform.tfvars.example` as an example

```shell
cp test/fixtures/shared/terraform.tfvars.example test/fixtures/shared/terraform.tfvars
```

The `terraform.tfvars` in each fixture directory is already symlinked to this one shared file.

2. Populate the variables with values appropriate for your test environment (i.e. `project_id`, `service_account.email`)
3. Download a Service Account key with the necessary [permissions](#permissions) and put it in the module's root directory with the name credentials.json.

## Running Tests

From the root of the module, run

```
make test_integration_docker
```

to build the container and run through all the test suites. Note that this will take some time (> 20 minutes).

You can also run each test case individually and interactively in the Docker container:

```
make docker_run
```

The root directory of the module will be mounted to `/cft/workdir` in the container. For example, to run the `mig-autoscaler` test suite:

```
bundle exec kitchen test mig-autosaler
```

or

```
bundle exec kitchen create mig-autoscaler
bundle exec kitchen converge mig-autoscaler
bundle exec kitchen verify mig-autoscaler
bundle exec kitchen destroy mig-autoscaler
```

## Permissions

The service account used to execute tests for this module should have the following roles:
- [`roles/compute.admin`](https://cloud.google.com/iam/docs/understanding-roles#compute-engine-roles)
- [`roles/iam.serviceAccountUser`](https://cloud.google.com/iam/docs/understanding-roles#service-accounts-roles)


## License
[![FOSSA Status](https://app.fossa.com/api/projects/git%2Bgithub.com%2Fboeyeb%2Fterraform-google-vm.svg?type=large)](https://app.fossa.com/projects/git%2Bgithub.com%2Fboeyeb%2Fterraform-google-vm?ref=badge_large)