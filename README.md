# Installing Vagrant — Complete Guide

A step-by-step guide to setting up a Linux virtual machine using Vagrant and VirtualBox on Windows, and connecting it to VS Code.

---

## Prerequisites

- A Windows PC
- Git Bash installed
- Internet connection

---

## Step 1 — Install Oracle VirtualBox

Download and install Oracle VirtualBox from the official site:

> https://www.virtualbox.org/wiki/Downloads

Run the installer and follow the on-screen steps.

---

## Step 2 — Install Vagrant

Download Vagrant from the official HashiCorp site:

> https://developer.hashicorp.com/vagrant/install

Run the installer normally, then **restart your computer** before continuing.

---

## Step 3 — Download the Vagrant Files

Download the two configuration files from this repository:

> https://github.com/harshit391/Linux-Vagrant-Files

Place both files (`Vagrantfile` and `pg_config.sh`) into a **separate, dedicated folder** on your machine.

---

## Step 4 — Start the Virtual Machine

1. Open the folder containing the Vagrant files in **Git Bash**
2. Run the following command:

```bash
vagrant up
```

> This will take a while — the first run downloads the Linux box image. Be patient.

3. When VirtualBox prompts you with any network/firewall dialogs, **allow everything**.

---

## Step 5 — SSH into the VM

Once `vagrant up` finishes, connect to your Linux VM:

```bash
vagrant ssh
```

Your terminal prompt will change, confirming you are now inside the Linux VM.

---

## Step 6 — Install GCC (Optional)

To install the GCC compiler inside the VM:

```bash
sudo apt install gcc
```

---

## Step 7 — Exit and Stop the VM

To exit the SSH session:

```bash
exit
```

To shut down the VM:

```bash
vagrant halt
```

> **Note:** Do not try to start or manage the VM directly from the VirtualBox GUI. Always use Vagrant commands from Git Bash.

---

## Step 8 — Connect Vagrant to VS Code

Vagrant automatically creates a **shared folder** that is accessible both from your Windows machine and from inside the VM.

### How it works

| Location | Path |
|----------|------|
| Windows (your machine) | The folder where your `Vagrantfile` lives |
| Inside the VM | `/vagrant` |

### Access the shared folder in the VM

```bash
cd /vagrant
ls
```

Any file you see here is the same file in your Windows folder — edits are reflected instantly on both sides.

### Open the shared folder in VS Code

1. Open VS Code
2. Go to **File → Open Folder**
3. Navigate to the folder containing your `Vagrantfile`
4. Open it

Now whatever you create or edit in VS Code is immediately accessible inside the VM at `/vagrant`. This is the recommended workflow for editing code.

---

## Quick Command Reference

| Command | Description |
|---------|-------------|
| `vagrant up` | Start (and provision) the VM |
| `vagrant ssh` | SSH into the running VM |
| `vagrant halt` | Shut down the VM |
| `vagrant reload` | Restart the VM |
| `vagrant destroy` | Delete the VM entirely |
| `cd /vagrant` | Access the shared folder (run inside VM) |
| `exit` | Exit the SSH session |

---

## Troubleshooting

- **`vagrant up` hangs or times out** — Make sure VirtualBox is installed and your BIOS has virtualization (VT-x/AMD-V) enabled.
- **Shared folder not mounting** — Ensure VirtualBox Guest Additions are installed. Try `vagrant reload --provision`.
- **SSH connection refused** — Wait a moment and retry; the VM may still be booting.
