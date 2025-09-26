---

# 🍎 MacOS-on-VBox

All links are for **Arch Linux**, but you can also do this on any other Linux distro (or even Windows).

---

## 📥 Stuff you need to download

* [VirtualBox](virtualbox-host-dkms)
* MacOS ISO (tested with version **11**)

---

## ✅ Tested MacOS versions

* **Big Sur** ✔️
* **Tahoe** ❌

---

## ⚙️ My Config

You can use my pre-made config file: **MacOS.ova**

Specs I used:

* 8 Cores 🖥️
* 16 GB RAM 💾
* Hardware acceleration: **On** ⚡

---

## 🔧 Things you need to change/enable

To make MacOS work, run these commands in your terminal (Linux only — can be converted for Windows with a little help from Perplexity AI 😉):

```bash
# Set CPU features
vboxmanage modifyvm "MacOS" --cpuidset 00000001 000106e5 00100800 0098e3fd bfebfbff

# Mimic Mac hardware
vboxmanage setextradata "MacOS" "VBoxInternal/Devices/efi/0/Config/DmiSystemProduct" "iMac19,3"
vboxmanage setextradata "MacOS" "VBoxInternal/Devices/efi/0/Config/DmiSystemVersion" "1.0"
vboxmanage setextradata "MacOS" "VBoxInternal/Devices/efi/0/Config/DmiBoardProduct" "Iloveapple"

# SMC device key
vboxmanage setextradata "MacOS" "VBoxInternal/Devices/smc/0/Config/DeviceKey" \
"ourhardworkbythesewordsguardedpleasedontsteal(c)AppleComputerInc"
vboxmanage setextradata "MacOS" "VBoxInternal/Devices/smc/0/Config/GetKeyFromRealSMC" 0

# AMD CPUs only → fake Intel profile
vboxmanage modifyvm "MacOS" --cpu-profile "Intel Core i7-6700K"

# Timing fix
vboxmanage setextradata "MacOS" "VBoxInternal/TM/TSCMode" "RealTSCOffset"

# Graphics tweaks
VBoxManage modifyvm "MacOS" --graphicscontroller vmsvga
VBoxManage modifyvm "MacOS" --accelerate3d on
VBoxManage modifyvm "MacOS" --vram 256
```

---

## 💿 Configuring the VM

1. Import the **MacOS.ova** config.
2. Add the MacOS ISO (I used the Big Sur torrent).
3. Create a virtual drive of around **~80 GB**.

---

## 🍏 Inside MacOS Setup

* Boot the VM (⚠️ it may take a while ⏳).
* Open **Disk Utility** and format the drive using **APFS**.
  (Don’t worry if it looks slightly different from my screenshot 👇)

<img width="1596" height="899" alt="Screenshot From 2025-09-26 21-14-53" src="https://github.com/user-attachments/assets/923a1cfe-a934-4369-9c93-02267581cc8e" />

* Close Disk Utility and start installing **Big Sur**.

---

## 🎉 You’re done!

⚠️ Heads-up: it’s *super slow* without GPU passthrough (AMD-only).
The setup is laggy at first but gets better after installation.

I had to figure this out bit by bit... hope it helps you too! 💖

- *Kira* 🌸

---
