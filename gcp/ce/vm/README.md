# Create a virtual machine in gcp instance using terraform

Required: 

- A google cloud account, if you don't have one yet, create a free [google cloud account](https://cloud.google.com/free/).
- Computer Engine API must be enabled
- Terraform

Login to your account and go to cloud shell in the top right corner. terraform should be already installed, you could check it by

```bash
$ terraform version
```

## What is terraform?

Terraform is a tool for building, changing, and versioning infrastructure safely and efficiently. Terraform can manage existing, popular service providers as well as custom in-house solutions.

You could check the authenticated account

```bash
$ gcloud auth list
```

And the list of projects

```bash
$ gcloud config list project
```

## Creating the VM configuration file

Start the editor in order to continue creating terraform configuration file. Then create a new file named instance.tf and add the following content into it:

```bash
resource "google_compute_instance" "default" {
  project      = "<your project id>"
  name         = "terraform"
  machine_type = "n1-standard-1"
  zone         = "us-central1-a"

  boot_disk {
    initialize_params {
      image = "debian-cloud/debian-9"
    }
  }

  network_interface {
    network = "default"
    access_config {
    }
  }
}
```

Replace the placeholder with your project id retrieved in the previous command. 

## Initialization

The first command to run for a new configuration -- or after checking out an existing configuration from version control -- is terraform init. This will initialize various local settings and data that will be used by subsequent commands.

At this stage terraform downloads the required Google provider plugin.

The terraform plan command is used to create an execution plan, enter terraform plan, so that terraform knows which resources are going to be created or modified.

**Hint**: You could use this command always before git commit in order to ensure the current state of your resources.

## Applying the changes

In the current folder where the instance.tf is located enter terraform apply.

After that terraform will report the created virtual machine instance.
You could show the current configuration at any time by using the following command

```bash
$ terraform show
```

### Check the created Virtual machine instance in console

Go to Compute Engine from the left menu and select VM Instances, a new vm instance named terraform should be in running state.
You could connect into it using ssh using your google cloud credential in the current web browser!

### Delete the Virtual machine instance

This could be done by invoking the following command

```bash
$ terraform destroy
```

This will delete the virtual machine istance and the related resources.