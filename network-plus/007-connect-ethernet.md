# Connect a Workstation to Structured Cabling

**Exam objective:** N10-009 1.5: Transmission media and transceivers · 2.4: Physical installation
**Course location:** Module 2.2, Lab 9
**Environment:** Simulated office workbench and Windows 11
**Result:** 100%

## Objective

Connect an office computer (Office 1) to the building's wired network through the Ethernet wall outlet, then confirm it has internet access.

## Topology

```mermaid
graph LR
    PC[Office 1 PC] ---|Cat6a patch cable<br/>shielded RJ45| WP[Wall plate]
    WP -. horizontal cabling in walls .- PP[Patch panel] --- SW[Switch] --- R[Router] --- ISP((Internet))
```

The dotted section is the building's existing cabling, which was already in place.

## What I did

1. Switched to the rear view of the Office 1 computer.
2. Picked a **Cat6a** patch cable with **shielded RJ45** connectors.
3. Plugged one end into the computer's Ethernet port and the other into the Ethernet jack on the **wall plate**.
4. Opened **Settings → Network & internet** in Windows 11 and confirmed an active internet connection.

## Key concepts

- **Structured cabling:** In an office the PC doesn't connect straight to a switch. The path is:
  - **Patch cable** from the PC to the **wall plate**
  - **Horizontal cable** inside the walls to a **patch panel** in the telecom closet (IDF)
  - **Patch cable** from the patch panel to the **switch**

  The 100 m Ethernet limit covers that whole run from end to end: up to 90 m of horizontal cable plus up to 10 m of patch cables in total.
- **Cat6a vs. other categories:** Cat6a carries **10GBASE-T up to 100 m**. Cat6 only reaches about 55 m at 10 Gbps, and Cat5e is limited to 1 Gbps. Cat6a here is more than a desktop needs today, but the cabling won't hold back future upgrades.
- **Wall plate jacks can look alike.** An RJ45 data jack looks a lot like an RJ11 phone jack. RJ45 is wider, with 8 pins; RJ11 is narrower, with 4–6. Plugging into the wrong one is a common "no network" cause.
- **Plug in, then verify:** A connected cable isn't proof of a working connection. Check the link lights, then confirm the OS has a connection.

## Takeaways

The simplest lab so far, and it covers the most common physical fix there is. Knowing the full path from desk to closet tells you where to look when one desk is down: the patch cable, the jack, the horizontal run, the patch panel or the switch port.
