# Deploying NAT Gateway for Outbound Access

## Lab Overview

In this lab, you will:

* Provision a NAT Gateway in Azure
* Attach a Public IP or IP Prefix
* Associate the NAT Gateway with a subnet
* Configure the TCP idle timeout
* Deploy a VM and verify outbound internet access through the NAT Gateway

> **Skill Level:** Beginner
> **Tools Used:** Azure Portal, Azure CLI in Cloud Shell

---

## Part 1: Prerequisites

### Step 1: Open Azure Cloud Shell

* Go to [https://shell.azure.com](https://shell.azure.com)
* Choose **Bash**

### Step 2: Create a Resource Group

Replace `yourname` with your name without spaces.

```bash
az group create --name rg-yourname-nat-lab --location eastus
```

### Step 3: Create a VNet and Subnet

```bash
az network vnet create \
  --resource-group rg-yourname-nat-lab \
  --name vnet-nat-lab \
  --address-prefix 10.20.0.0/16 \
  --subnet-name subnet-nat \
  --subnet-prefix 10.20.1.0/24
```

---

## Part 2: Create NAT Gateway

### Step 4: Create a Public IP

```bash
az network public-ip create \
  --resource-group rg-yourname-nat-lab \
  --name nat-public-ip \
  --sku Standard \
  --allocation-method Static
```

### Step 5: Create NAT Gateway

```bash
az network nat gateway create \
  --resource-group rg-yourname-nat-lab \
  --name nat-gateway-demo \
  --public-ip-addresses nat-public-ip \
  --idle-timeout 10 \
  --location eastus
```

> **Note:** The idle timeout is set to 10 minutes. You can adjust this value if needed.

### Step 6: Associate NAT Gateway with Subnet

```bash
az network vnet subnet update \
  --resource-group rg-yourname-nat-lab \
  --vnet-name vnet-nat-lab \
  --name subnet-nat \
  --nat-gateway nat-gateway-demo
```

---

## Part 3: Create VM to Test Outbound IP

### Step 7: Create a VM in Subnet

```bash
az vm create \
  --resource-group rg-yourname-nat-lab \
  --name vm-nat-test \
  --vnet-name vnet-nat-lab \
  --subnet subnet-nat \
  --image Ubuntu2204 \
  --admin-username azureuser \
  --generate-ssh-keys \
  --public-ip-sku Standard
```

Take note of the location of the keys shown in the Cloud Shell for example:

```bash
SSH key files '/home/user/.ssh/id_rsa' and '/home/user/.ssh/id_rsa.pub' have been generated under ~/.ssh to allow SSH access to the VM. If using machines without permanent storage, back up your keys to a safe location.
```
---

## Part 4: Verify Outbound IP

### Step 8: SSH into the VM

```bash
az vm show \
  --resource-group rg-yourname-nat-lab \
  --name vm-nat-test \
  --show-details \
  --query publicIps -o tsv
```

```bash
ssh azureuser@<public-ip>
```

Enter `yes` when asked `Are you sure you want to continue connecting (yes/no/[fingerprint])?`

### Step 9: Check Outbound IP

From inside the VM:

```bash
curl ifconfig.me
```

> You should see the public IP assigned to the NAT Gateway.

---

## Cleanup 

Type `exit` to close the VM session
 Then run the following command:
```bash
az group delete --name rg-yourname-nat-lab --yes --no-wait
```

---

## Lab Complete

You have successfully:

* Deployed a NAT Gateway
* Connected it to a subnet
* Deployed a VM and confirmed its outbound IP via NAT
