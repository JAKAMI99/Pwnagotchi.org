+++
tags = ["documentation"]
title = "first run (linux)"
weight = 57
+++

## First run
Congratulations, your SD card should be now ready for boot! Safely remove your SD card from your computer, and insert it into your Raspberry Pi. There are two USB ports on your Pi 0, labeled as "PWR IN" and "DATA", see this image:

![RPi 0 USB ports](https://github.com/pwndevelopers/community-wiki/assets/21370314/8de186f5-e095-47af-8e2c-e39705aac432)

Insert your USB cable into the "DATA" port, which is shown in the image above, and connect it to your PC. The green LED on your Pi should start blinking quickly for a while, that means it is starting up. In the meantime, you can enable Bluetooth and Hotspot on your phone, so you can get up and running. The process of booting up for the first time can take few minutes or up to tens of minutes depending on your SD card and your pwnagotchi's CPU, so give it a little while. In the meantime, you can make yourself a coffee, have a snack, or join our [Discord](https://discord.gg/PgaU3Vp) community and get to know the most amazing people!

## SSH into your pi
This example is based on Manjaro OS with Xfce desktop envorinment however this should be similar, if not the same, on other distrobutions. First, open terminal and type in `ip -o link show | awk -F': ' '{print $2}'`. You should see a list of ethernet interfaces active. Take note of what are available, in my case, I have `eno1` and `lo` (the `lo` interface will always be there, as it is a loopback virtual adapter, other distributions might differ in naming however this is highly unlikely). Then, connect your pwny and wait for it to boot. Run `ip -o link show | awk -F': ' '{print $2}'` again, and you should see a new interface, in my case it was named `enp0s20f0u2u2`, that is your pwny. Take note of that.

Open your Network Manager, you should see a window like this, the amount and names of connections will probably differ but that is okay:

![Xfce Network Manager](https://github.com/pwndevelopers/community-wiki/assets/21370314/9eaf909c-cf86-49b8-8463-26c2b36d90d2)

Click the "+" at the bottom. New window will pop up, asking you to choose connection type. Set "Ethernet" and create.

In this new window, you can enter connection name at the top, and select device that you figured out earlier (in my case it was the `enp0s20f0u2u2`):

![Network manager Ethernet settings](https://github.com/pwndevelopers/community-wiki/assets/21370314/fa0c6318-dae4-44cd-9fa1-1c4986abc8ff)

After that, head over to "IPv4 Settings", change method to "Manual" and enter details as on the screenshot:

![Network Manager IPv4 settings](https://github.com/pwndevelopers/community-wiki/assets/21370314/64ba6e9f-e11e-4e18-a420-5b280ca713c0)

After that, you can save and your connection should work. Open the terminal, and type in `ssh <username>@10.0.0.2`, where `<username>` is whatever username you have specified in the Imager. If you haven't, the default is `pi`. Enter the password you have specified in the Imager, if you haven't, then the default is `raspberry`.

## Connection sharing

To share internet connection from your computer to your pwnagotchi, all you have to do is download this [script](https://raw.githubusercontent.com/jayofelony/pwnagotchi/master/scripts/linux_connection_share.sh) using the following command:

```sh
wget https://raw.githubusercontent.com/jayofelony/pwnagotchi/master/scripts/linux_connection_share.sh
```

Once downloaded, you should run it with `sudo` (check the source before doing that), passing the pwnagotchi's interface as the first argument and your computer's network interface as the second argument, like this:

```sh
sudo ./linux_connection_share.sh enp0s20f0u2u2 eno1 # WARNING: change the parameters name using your interfaces' names!
```

After that, your pwnagotchi should be able to connect to internet via USB connection. The script adds some iptables rules to your computer so the packets coming from pwnagotchi's interface are forwarded to your internet connected interface.

### Common issues


**> New Network Interface after every boot (MAC-Adress)**

This happens, because the pwnagotchi generates a new MAC-address after every reboot. To set a static MAC-address see [Common Issues](/common-issues/)

**> After computer reboot, my Pwnagotchi doesn't connect to internet anymore**

This also happens because the pwnagotchi generates a new MAC-address after every boot. Fix: [Common issues](/common-issues/)




