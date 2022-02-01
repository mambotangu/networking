## Task 1. Set up Terraform and Cloud Shell
Configure your Cloud Shell environment to use Terraform.

### Install Terraform
Terraform is now integrated into Cloud Sell. Verify which version is installed.

In the Cloud Console, click Activate Cloud Shell (Cloud Shell).

If prompted, click Continue.

Confirm that Terraform is installed by running the following command:
    terraform --version

Create a directory for your Terraform configuration by running the following command: mkdir tfnet

Create a file, provider.tf in the tfnet folder touch provider.tfnet

Create a new configuration and define managementnet.

# Create the managementnet network
resource [RESOURCE_TYPE] "managementnet" {
name = [RESOURCE_NAME]
auto_create_subnetworks = "false"
}

In managementnet.tf, replace [RESOURCE_TYPE] with "google_compute_network" and  [RESOURCE_NAME] with "managementnet"

## Add managementsubnet-us to the VPC network.

### Create managementsubnet-us subnetwork
resource "google_compute_subnetwork" "managementsubnet-us" {
name          = "managementsubnet-us"
region        = "us-central1"
network       = google_compute_network.managementnet.self_link
ip_cidr_range = "10.130.0.0/20"
}

### Configure the firewall rule
#### Add a firewall rule to allow HTTP, SSH, and RDP traffic on managementnet
resource [RESOURCE_TYPE] "managementnet-allow-http-ssh-rdp-icmp" {
name = [RESOURCE_NAME]
network = google_compute_network.managementnet.self_link

allow {
    protocol = "tcp"
    ports    = ["22", "80", "3389"]
    }
source_ranges = ["0.0.0.0/0"]
allow {
    protocol = "icmp"
    }
}

replace [RESOURCE_TYPE] with "google_compute_firewall" and [RESOURCE_NAME] with "managementnet-allow-http-ssh-rdp-icmp"