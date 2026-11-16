# Install a NIC and Reconnect to Ethernet

**Exam objective:** N10-009 1.5: Transmission media and transceivers · 2.4: Physical installation
**Course location:** Module 2.1, Lab 7
**Environment:** Simulated hardware workbench and Windows 11
**Result:** 100%

## Objective

Get a workstation (Office2) back on the wired network. I installed a new Gigabit Ethernet network adapter, moved the network cable from the built-in port to the new card, and confirmed the machine could reach both the local network and the internet.

## Topology

```mermaid
graph LR
    O2[Office2<br/>New 1000BASE-T PCIe NIC] ---|Cat5e, shielded RJ45| SW[Switch / LAN]
    SW --- R[Router] --- ISP((Internet))
```

## What I did

1. **Picked the right adapter.** The shelf had several network adapters. I chose the one with the fastest Ethernet standard, **1000BASE-T (Gigabit)**, on a **PCIe** interface.
2. **Installed the card.** In the motherboard view I seated the adapter in a free **PCIe expansion slot**.
3. **Moved the network cable.** At the back of the computer I unplugged the **Cat5e** cable's shielded RJ45 connector from the onboard NIC and plugged it into the new adapter's port.
4. **Powered on and checked.** After Windows 11 booted, I opened **Settings → Network & Internet**. It showed an active connection to the local network and the internet.

## Key concepts

- **Reading Ethernet standard names:** `1000BASE-T` breaks down as:
  - `1000` = 1000 Mbps (1 Gbps)
  - `BASE` = baseband signaling
  - `T` = twisted-pair copper

  | Standard | Speed | Common cable | Max distance |
  |----------|-------|--------------|--------------|
  | 100BASE-TX | 100 Mbps | Cat5 / Cat5e | 100 m |
  | 1000BASE-T | 1 Gbps | Cat5e / Cat6 | 100 m |
  | 10GBASE-T | 10 Gbps | Cat6 (≈55 m) / Cat6a (100 m) | up to 100 m |

- **Cat5e is enough for Gigabit.** It supports 1000BASE-T up to 100 m, and 1000BASE-T uses all four wire pairs. Plain Cat5 is officially rated for 100 Mbps, so Cat5e is the minimum for Gigabit.
- **Shielded vs. unshielded:** A shielded (STP/FTP) connector and cable resist electromagnetic interference. That helps near motors, fluorescent lighting or power runs. For the shielding to work, the connector has to be grounded through the jack.
- **PCIe:** The current standard expansion bus. A NIC fits in an x1 slot or any larger one. PCIe has replaced legacy PCI.
- **Moving the cable is part of the fix.** A new NIC does nothing until the cable is in it. A common mistake is installing the card and leaving the cable in the old, dead port.

## How I'd confirm it outside the simulator

```powershell
Get-NetAdapter                # is the new adapter present, "Up", and at 1 Gbps?
ipconfig /all                 # did it get a DHCP address, gateway, and DNS?
ping <default gateway>        # local network reachability
ping 8.8.8.8                  # internet reachability (past the router)
nslookup example.com          # name resolution
```

I'd also check the **link/activity LEDs** on the NIC and the switch port. If they're off, it's a Layer 1 problem: the cable, the port or the card.

## Takeaways

This was a Layer 1 repair: the right card, the right slot, the right cable and the right port, then checking upward through the layers. "No network" tickets often end with a hardware swap like this, and knowing what the cable and standard can carry stops you from installing a Gigabit card on a cable that can't run at Gigabit.
