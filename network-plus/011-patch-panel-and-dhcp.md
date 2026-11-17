# Patch an Office Drop and Enable DHCP

**Exam objective:** N10-009 2.4: Physical installation · 3.4: Network services (DHCP)
**Course location:** Module 2.3, Lab 8
**Environment:** Simulated office floor and networking closet, Windows 11
**Result:** 100%

## Objective

Bring Office 1 online from start to finish: patch its cable run into the switch in the networking closet, connect the workstation to the wall outlet, and set the workstation to get its IP and DNS settings automatically.

## Topology

```mermaid
graph LR
    PC[Office 1 workstation<br/>DHCP] ---|Cat6a patch| WO[Wall outlet]
    WO -. horizontal run .- PP["Patch panel<br/>port 'Off 1'"]
    PP ---|Cat6a patch| SW[Cisco switch<br/>port 3]
    SW --- NET[Network / DHCP server / Internet]
```

## What I did

1. **In the networking closet:** Patched the **"Off 1"** (Office 1) patch panel port to **port 3** on the Cisco switch with a Cat6a patch cable.
2. **In Office 1:** Connected the workstation's Ethernet port to the open jack on the wall outlet with a Cat6a cable.
3. **On the workstation:** In **Settings → Network & internet → Ethernet → IP assignment**, changed the setting from manual to **Automatic (DHCP)** and saved.
4. **Checked:** Network & internet showed **Connected** with the globe icon, meaning internet access.

## Key concepts

- **Both ends need patching.** The horizontal cable from a wall outlet ends at a patch panel, not at a switch. The jack isn't live until someone patches that panel port into a switch port. Many "dead jack" tickets come down to a missing patch cable in the closet.
- **Patch panel labels:** Ports are labeled by location ("Off 1", "Exec 1", "Lobby") so a tech can trace any desk to its closet port without tracing cables by hand.
- **Physical fix plus logical fix:** The cabling gave the PC a link, but it still needed a valid IP configuration. Setting it to DHCP let the network's server assign the address, mask, gateway and DNS.
- **DHCP for IP and DNS:** Windows can set the IP and DNS separately. Both should be automatic unless there's a reason to hard-code DNS, such as pointing at an internal DNS server or a filtering resolver.

## Takeaways

This lab was the whole desk-to-switch path in one ticket: closet patching, the desk cable and the host's IP settings. It's the same flow I used in the troubleshooting methodology lab, done here from the start.
