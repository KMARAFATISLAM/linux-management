## Azure Virtual Machine Setup Documentation
### Initial Setup

1. Created account at portal.azure.com using HAMK student credentials
2. Navigated to Azure Portal homepage (portal.azure.com/#home)
3. Selected "Create a resource"
4. Clicked "Create" under virtual machine option

### Basic Configuration

* Resource Group: robotics
* Virtual Machine Name: Linux management
* Region: (Europe) North Europe
* Availability Options: No infrastructure redundancy required
* Image: Ubuntu Server 24.04 LTS - x64 Gen2
* VM Architecture: x64
* Size: Standard_B2ls_v2 (2 vcpus, 4 GiB memory)

### Authentication Settings

* Authentication Type: SSH public key
* Username: mrrafsan
* SSH Public Key Source: Generate new key pair
* SSH Key Type: RSA SSH Format
* Key Pair Name: linux-management_key
* Inbound Ports:
* * HTTP (80)
* * HTTPS (443)
* * SSH (22)

### Disk Configuration

* OS Disk Type: Standard SSD (locally-redundant storage)
* Delete with VM: Enabled
* Key Management: Platform-managed key

### Networking

* Used default networking settings
* Delete NIC when VM is deleted: Enabled
* Accelerated Networking: Not available
* DNS Configuration:
* * DNS name label: mrrafsan-lab-robotics

### Management

* Auto-shutdown: Enabled
* Timezone: Helsinki
* Shutdown Time: 5:00 PM
* Email Notification: Disabled

### Final Steps

- Reviewed configuration
- Created VM