# KVM Installation and Configuration Commands

Run these commands in an Ubuntu terminal.

## 1. Update Ubuntu

```bash
sudo apt update && sudo apt upgrade -y
```

## 2. Check CPU virtualization support

```bash
sudo grep -c 'svm\|vmx' /proc/cpuinfo
```

A result greater than `0` indicates that virtualization support is exposed to Ubuntu.

## 3. Install the KVM checker

```bash
sudo apt install cpu-checker
```

## 4. Check whether KVM is available

```bash
kvm-ok
```

The expected successful message is: `KVM acceleration can be used`.

## 5. Install KVM, QEMU, and Virtual Machine Manager

```bash
sudo apt install qemu-kvm virt-manager libvirt-daemon-system libvirt-clients bridge-utils -y
```

## 6. Enable and start libvirt

```bash
sudo systemctl enable libvirtd
sudo systemctl start libvirtd
```

## 7. Add your user to the required groups

Replace `kishore` with your actual Ubuntu username if it is different.

```bash
sudo usermod -aG kvm kishore
sudo usermod -aG libvirt kishore
```

## 8. Check libvirt service status

```bash
sudo systemctl status libvirtd
```

Press `q` to exit the status screen.

## 9. Apply group membership

Log out and log back in, or restart Ubuntu, so the new group membership takes effect.
