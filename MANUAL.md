# FlatJack manual

**English** | [Українська](MANUAL.uk.md) · [Quick start](README.md)

Everything FlatJack does, and the details that matter. Things marked with a version, such as **(1.4.0)**, are new in that version.

- [The screen](#the-screen)
- [The web page](#the-web-page)
- [Charging modes](#charging-modes)
- [How automatic charging works](#how-automatic-charging-works)
- [Charge limit](#charge-limit)
- [Generator](#generator)
- [Several batteries](#several-batteries)
- [Changing BMS settings](#changing-bms-settings)
- [Calibration and BMS commands (1.0.0)](#calibration-and-bms-commands-100)
- [Alarms](#alarms)
- [How long the battery lasts](#how-long-the-battery-lasts)
- [Energy (1.2.0)](#energy-120)
- [Charge history](#charge-history)
- [Bluetooth](#bluetooth)
- [Home Assistant](#home-assistant)
- [ESPHome](#esphome)
- [Updates and restarts](#updates-and-restarts)
- [Safety and limits](#safety-and-limits)
- [Troubleshooting](#troubleshooting)
- [All screens](#all-screens)
- [For the technically minded: the web API](#for-the-technically-minded-the-web-api)

---

## The screen

Five tabs, chosen with the icons on the left: home, battery, charging, history (1.4.0), settings. The bar on top always says in one sentence what is going on; on the right is the clock. **Tap the bar (1.4.0)** for every alarm and warning by name, as the web page lists them: each battery's alarms, protections with their countdown, a silent battery or Flatpack, the Flatpack's own alarms.

<p>
<img src="docs/img/manual/en/screen-home-a.png" alt="Home: charging" width="49%">
<img src="docs/img/manual/en/screen-home-b.png" alt="Home: mains outage" width="49%">
</p>

**Home.** At the top, where the power comes from and where it goes: the Flatpack's card (mains voltage, the power it gives, its voltage and current), the house ("Load", and whether it is fed from the mains, the battery, the generator or both), and the lines between them: green while the mains charges or feeds, orange while the battery feeds. Below, the battery: charge %, capacity left, the power going in or out, and either the time to full charge, the time to the charge limit, or how long the battery lasts (see [How long the battery lasts](#how-long-the-battery-lasts)). The last line is the pack's voltage, current, temperature and cell spread. **Tap the Flatpack's card (1.4.0)** for its details: status, mains, output, the setpoint with OVP, the power limit, inlet and outlet temperature and its alarms by name.

**The top bar** turns orange for a warning and red for an alarm; with several alarms the first is named and "+N" counts the rest. Its words:
- the charging phase in plain words: **Charging**, **Topping up**, **Full**, **SOC limit**, **Hold**, **Waiting**, **Manual mode**, **Charging off**, **Keeping charge**;
- **On battery**: the mains is off and the battery feeds the house (a normal state, not a fault);
- **Discharge off**: no battery has its discharge switch on, so the battery would not feed the house;
- a battery alarm (see [Alarms](#alarms)) or a Flatpack fault: "Mains voltage too high", "Flatpack overheated", "Flatpack fan", "Overvoltage protection" and others;
- **No link** / **Looking for battery…** while no BMS answers.

**Top right, beside the clock (1.0.0):** a plug while the BMS answers over its cable, the Bluetooth sign while it answers over Bluetooth, a crossed-out battery while no battery answers.

<p>
<img src="docs/img/manual/en/screen-home-d.png" alt="Home: SOC limit" width="49%">
<img src="docs/img/manual/en/screen-home-g.png" alt="Home: an alarm" width="49%">
</p>

**Without a battery** (none connected, or the Flatpack used on its own) the screen becomes the charger's own: output voltage, current, power, mains and temperature.

<img src="docs/img/manual/en/screen-home-f.png" alt="Home: no battery" width="49%">

**Battery tab.** Three views: **General** (voltage, current, temperature, capacity, SOH, cycles), **Cells** (a 4×4 grid; the highest cell orange, the lowest blue; tap **Cells** again for cells 17–32), **Switches** (1.4.0: the BMS's charge, discharge and balancing switches; a tap asks first and says what follows, and **Yes** writes it to the BMS as the web page's switches do; over Bluetooth they are only shown). With 2 or more batteries a chip beside the views shows "1 of 2": tap it for the next battery. The footer says what the battery's switches do (charge off, discharge off, heating, balancing) and the MOSFET and Flatpack temperatures (orange above 65 °C).

<p>
<img src="docs/img/manual/en/screen-bat-a.png" alt="Battery: general" width="32%">
<img src="docs/img/manual/en/screen-cells-a.png" alt="Battery: cells" width="32%">
<img src="docs/img/manual/en/screen-sw-a.png" alt="Battery: switches" width="32%">
</p>

**Charging tab.** The mode on top (**Off / Keep / Auto / Manual**; a tap asks first and says what follows). In **Auto**: **Charge to** (the SOC limit, 100 % = charge fully) and **Battery current**. In **Manual**: the Flatpack's voltage and current, sent with **Apply**. **Apply** keeps the over-voltage limit at least 0.5 V above the voltage, as the web page's quick control does. The last row is the **Generator**: a switch and its power, 100–4000 W (see [Generator](#generator)). Holding + or − steps fast; the value is sent 0.7 s after the last step. The footer says the voltages ("Charging to 55.2 V, then 53.6 V") or why it pauses. In **Auto**, **tap that line (1.4.0)** for the charge stages: FlatJack's phases with their voltages and times (the current one green), the BMS's stage and its time, the setpoint now, and the **Two-stage charge** switch (see [How automatic charging works](#how-automatic-charging-works)).

<p>
<img src="docs/img/manual/en/screen-charge-a.png" alt="Charging: auto" width="32%">
<img src="docs/img/manual/en/screen-charge-h.png" alt="Charging: manual" width="32%">
<img src="docs/img/manual/en/screen-sh-stages-a.png" alt="Charge stages" width="32%">
</p>

**History tab (1.4.0).** **Day** and **Week**: charge %, battery power (into the battery green, out of it orange) and voltage on one time axis, each chart with its highest and lowest value; a gap where nothing was recorded. **Energy**: the Flatpack's kWh for the last seven days as bars, today first; tap a day for its numbers, in the web page's words (see [Energy](#energy-120)). The charts need internet time.

<p>
<img src="docs/img/manual/en/screen-hweek-a.png" alt="History: a week" width="49%">
<img src="docs/img/manual/en/screen-energy-a.png" alt="History: energy by day" width="49%">
</p>

**Settings tab.** **Flip the screen** (180°), **Turn the screen off** (never / 1 / 5 / 15 / 30 min; a touch wakes it and that touch does nothing else), **Backlight off too** (see the note below), **Connection** (1.4.0): **Wi-Fi** shows a QR code that opens the web page on a phone (while the setup network is open, it joins that network), with **Change**, which forgets the network and opens the setup network; **Bluetooth** lists the paired BMSes with **Forget**, and **Find a BMS** looks for one to **Add** (see [Bluetooth](#bluetooth)). The footer: the address, the version, the update button, the three languages.

<p>
<img src="docs/img/manual/en/screen-set-a.png" alt="Settings" width="49%">
<img src="docs/img/manual/en/screen-sh-ble-a.png" alt="Bluetooth from the screen" width="49%">
</p>

> [!NOTE]
> Waveshare's board revision 1.1 has a known fault: a few minutes with the backlight off leave a white glowing frame round the screen, which fades only slowly. Waveshare confirmed it; there is no software fix. That is why **Backlight off too** is off by default: the screen then turns black but the backlight stays on.

**If the battery goes silent in Auto** for 10 s, a dialog offers manual mode, once per outage. It closes by itself when the battery answers again, and charging carries on as before.

## The web page

Open http://flatjack.local/ or the board's address. Five tabs: **Overview, Cells, Charge, BMS, System**. On a phone the tabs are at the bottom. Light and dark follow your device. With 2 or more batteries, the Cells, BMS and System tabs have a "BMS 1 … 4" selector; everything you change there goes to the selected battery only.

<p>
<img src="docs/img/manual/en/web-phone.png" alt="Phone: overview" width="32%">
<img src="docs/img/manual/en/web-phone-cells.png" alt="Phone: cells" width="32%">
</p>

**Overview:** the power flow, the battery, the charging mode with a short explanation, cells, capacity, temperatures, the battery's switches, cycles and SOH, and the [charge history](#charge-history).

![Overview](docs/img/manual/en/web-home.png)

**Cells:** each cell's voltage and its deviation from the average, the balance-wire resistance of each, temperatures (T1–T5, MOSFET), balancing.

![Cells](docs/img/manual/en/web-cells.png)

**Charge:** the mode, the phases with what each is waiting for (voltage, timers, tail current), the settings (Charge to, Battery current, Flatpack power limit), the Flatpack's status, and manual control with OVP.

![Charge](docs/img/manual/en/web-charge.png)

**BMS:** the BMS's switches and every setting that can be changed: see [Changing BMS settings](#changing-bms-settings).

**System:** language, the controller (version, uptime, Wi-Fi signal, memory), the batteries found, Bluetooth, the BMS's details (model, versions, serial, manufacture date; (1.0.0) total run time and power-ons, its clock, time to sleep, power, voltage calibration, port protocols), Home Assistant (MQTT), firmware update, raw registers and **Reset Wi-Fi**.

![System](docs/img/manual/en/web-system.png)

## Charging modes

| Mode | What happens |
|---|---|
| **Off** | The Flatpack gives nothing (its voltage goes to 43.2 V); the battery feeds the house. |
| **Keep** | The battery neither charges nor discharges: the Flatpack feeds the house and the battery stays at its charge, whatever it is. Needs a battery. After a mains outage it does not recharge by itself. |
| **Auto** | Charges the battery from the BMS settings ([below](#how-automatic-charging-works)). Needs a battery. |
| **Manual** | You set the Flatpack's voltage, current and OVP. Without a battery this is the only mode. |

The mode is remembered. Auto and Keep come back by themselves after a restart or a power cut: FlatJack is meant to run unattended. Manual sends nothing after a restart until you press **Apply** again (the Flatpack meanwhile keeps its last setting).

## How automatic charging works

All numbers come from the BMS: **RCV** (charge voltage per cell), **RCV time**, **RFV** (float voltage per cell), **RFV time**, **float mode**, and «SOC 100 % at voltage». Change them in the BMS and charging follows at once.

**The BMS leads (1.3.0).** A JK BMS with firmware 19.10 or newer shows its own charge stage, and FlatJack follows it as an inverter would: Charging and Topping up at RCV × cells, Full at RFV × cells. The BMS decides when to move on: topping up starts once its own voltmeter reads more than RCV × cells (so FlatJack aims 0.07 V higher), lasts the RCV time by the BMS's own timer, which never pauses, and then goes to Full if the battery is above «SOC 100 % at voltage» × cells, else back to Charging. Full ends when the SOC has fallen by **Re-Bulk SOC** since Full began. With float mode off the BMS stays at Charging and asks for RCV for good. The Charge tab shows the BMS's stage and its time. The mode, charge limit, Keep, battery current, power cap and Hold work as below. There is no cell trim at the BMS's voltages: the BMS's own cell overvoltage protection guards the cells.
- At a high current the battery reaches RCV × cells early, so the BMS starts topping up, and shows 100 %, long before the battery is full. **Two-stage charge**, a switch on the Charge tab (off by default), helps: while the BMS is at Charging, FlatJack first holds the battery at the first stage below, until a minute of tail current, and only then gives RCV.
- Re-Bulk SOC may be as low as 1 % (it is on our test BMS): Full then ends after half a per cent of discharge, and a 30-minute topping up follows every small discharge. Raise it in the JK app, to 5–10 % for example.

**Without the BMS's stage** (firmware before 19.10) FlatJack runs its own stages:

1. **Charging (Bulk):** the battery takes your **Battery current** until its voltage reaches the topping-up voltage.
2. **Topping up (Absorb), two stages.**
   - First stage: 15 mV a cell under «SOC 100 % at voltage» (3.445 V → 54.88 V for 16 cells). Why: a JK BMS sets its SOC to 100 % the moment the battery reaches that voltage, whatever the current, so charging straight to RCV would show 100 % with the battery still taking 30 A. The stage ends after a minute in which the battery takes 5 % of its capacity or less (5 A for 100 Ah: the "tail current").
   - Second stage: RCV × cells for the **RCV time**. The timer counts only while the battery is within 0.25 V of that voltage and takes the tail current or less, so a mains outage or a load bigger than the Flatpack pauses it.
   - If «SOC 100 % at voltage» would not put the first stage between RFV and RCV, there is one stage, RCV × cells.
3. **Full (Float):** RFV × cells, if float mode is on in the BMS. With float mode off, topping up continues with no time limit.
4. **Charging again:** at SOC ≤ 90 %, but only after max(RFV time, 1 h) at Full, so a wrong SOC can't skip Full. After a mains outage at Full, charging starts again as soon as the mains is back if the BMS shows under 100 %.

**The voltage is the battery's own.** FlatJack charges by the BMS's voltmeter, not the Flatpack's: the wires, the fuse and the BMS's switches lose 0.3–0.5 V at 25–30 A. So the Flatpack's setpoint is raised by what is lost (at most 1 V, never closer than 0.5 V to its OVP, never more than 0.3 V above what it really gives) and comes down as the current falls. The Charge tab shows it as "Correction by the BMS voltmeter".

**A cell running ahead.** If a cell rises more than 10 mV over the phase's cell voltage while charging, the target goes down by up to 0.1 V per step, and comes back 0.05 V every 10 s.

**Current.** **Battery current** limits what goes into the battery; it is never more than 80 % of the BMS's charge overcurrent threshold, nor the Flatpack's 62.5 A. The Flatpack's limit is that plus what the house takes (worked out from the Flatpack's and the battery's currents), up to the same 80 % in total. OVP = the smaller of 58 V and cell OVP × cells.

**Hold.** If a BMS is silent, the settings look wrong or differ between batteries, or every charge switch is off, the Flatpack holds RFV × cells: the battery isn't charged but the house stays fed. Protection (temperature, overvoltage) is the BMS's job: it opens its charge switch. A Hold or Waiting of up to 10 minutes (for example the JK app over Bluetooth briefly cutting the cable link, or a mains blip) continues topping up or Full where it stopped; longer starts again from Charging. With the BMS leading, its stage comes back at once.

**Why this voltage now (1.1.0).** The Charge tab's "Setpoint breakdown" row adds it up: the stage's target, the cell trim and the BMS-voltmeter correction, e.g. «54.88 V (first stage) − 0.37 correction = 54.51 V», and says when the battery is already above the target, so no current goes in. Under it, the **Decision log** lists what the charger changed and why since the controller started, newest first: each phase change with its cause, the second stage, the topping-up timer starting or pausing, the cell trim, a mains outage, and your changes of mode and limits, each with the setpoint, the battery's voltage, current and SOC at that moment. A restart starts it again.

**After a restart** FlatJack's own stages start again from Charging (one extra topping up after each update); with the BMS leading, its stage simply carries on.

## Charge limit

**Charge to** below 100 %, for example 70 %, keeps the battery there:
- below the limit it charges;
- at the limit the Flatpack's voltage is adjusted every 5 s so the battery current stays near 0 A: the Flatpack carries the house, the battery idles;
- above the limit (you lowered it) the Flatpack steps back to (RFV − 0.1 V) × cells and the house drains the battery down to the limit;
- charging starts again at the limit − 3 %.

A JK BMS recalibrates its SOC only at full charge, so a permanent limit drifts: charge to 100 % now and then.

## Generator

For a small generator, set the Flatpack's **power limit**: on the screen the **Generator** switch and its power, on the web page (0 = none) or from Home Assistant `p_max`: 100–4000 W everywhere. Rule of thumb: about 80 % of the generator's rating (1.2 kW generator: 1000 W). The Flatpack draws about 5 % more from its AC side than it gives.

<p>
<img src="docs/img/manual/en/screen-home-n.png" alt="Home: on a generator" width="49%">
<img src="docs/img/manual/en/screen-charge-n.png" alt="Charging: generator on" width="49%">
</p>

What changes while the limit is on:
- **The Flatpack's current** is capped at limit ÷ setpoint voltage, in every mode, manual included. If the house takes more, the battery gives the rest.
- **Soft start.** The current rises to its maximum over at least 10 s (2 A/s at most) when charging starts, when the generator comes on and when a house load switches on; the battery covers the difference meanwhile. While a battery can take a load step (its discharge switch on), the limit also stays within about 3 A of what the Flatpack really gives. Without a battery the Flatpack gives what the house takes.
- **The end of the charge.** Once the BMS shows 100 %, topping up ends after one minute at the tail current instead of the RCV time. Before the BMS shows 100 % the RCV time stays. That saves up to the RCV time (30 min by default) of running a generator for 1–2 A. From the mains the RCV time stays, for the balancer.
- **If the controller dies,** the Flatpack falls back to 43.2 V: it stops charging rather than pull its full 2–3 kW from the generator. The cost: the battery feeds the house until the controller is back, and in manual mode charging resumes only with the next **Apply**.
- The screen's Flatpack card reads "Generator 224 V" instead of "Mains".

In Home Assistant an automation can set `p_max` when the generator starts and 0 when the mains is back.

## Several batteries

Up to 4 JK-PB batteries in parallel, one Flatpack.
- **Wiring:** all BMSes on one RS485 bus. RS485-2 has two RJ45 sockets: the board's cable goes into one, the next battery into the other, as with JK's parallel cable. **Each BMS needs its own DIP address 1–15.** JK's own parallel mode puts one BMS on address 0 as master: give it a free 1–15 as well; here FlatJack is the master.
- **Finding them:** with no battery answering, FlatJack tries every address 1–247 (about 80 s a round). Once one answers, it also tries 1–15 one every 3 s, so a battery added later appears within about 45 s. The addresses are remembered.
- **One pack:** SOC weighted by capacity, currents added, the worst cell, the warmest sensor. Each battery has its own row and its own settings.
- **Charging:** RCV, RFV, their times, float mode and the cell count must be equal on every battery; otherwise it holds and names the setting that differs. The charge current is at most 80 % of the sum of the charge overcurrent thresholds of the batteries whose charge switch is on. Parallel batteries don't share current evenly: leave some margin.
- **A silent battery** stops charging (Hold) until it answers or you remove it: **System → Batteries → Forget**. A single battery whose DIP address changed is found at the new address by itself.

## Changing BMS settings

On the **BMS** tab, tap a row, type the value and press **Write**. FlatJack writes it to the BMS and reads it back: the row then says **written, the BMS confirmed**, **the BMS keeps another value**, **the BMS refused the write** (outside what it accepts) or **no answer from the BMS**. One write at a time, for all batteries.

![BMS tab](docs/img/manual/en/web-settings.png)

![Three editors: a voltage, a signal's trigger, the voltage calibration](docs/img/manual/en/web-edit.png)

**What is checked before writing:**
- the range the BMS firmware accepts (for example balance current 0.3–2 A, charge OCP 1–200 A, temperatures within the BMS's limits);
- JK's own order: power-off < over-discharge < SOC 0 % < over-discharge recovery < overcharge recovery < SOC 100 % < RCV < overcharge, and each recovery on the right side of its threshold (temperatures included), heating off above heating on; a rule your BMS's current settings already break is left to the BMS;
- the charger's own: RFV ≤ RCV, and RCV × cells and RFV × cells within the Flatpack's 43.2–58 V, so a write can never park the charger in Hold.

**Groups on the tab:** Charge (RCV, RCV time, RFV, float mode, charge current and its delay / recovery), Cell protection (over/under-voltage and recovery, power-off, discharge current and delays, short circuit, pre-discharge, smart sleep), Balancing and SOC (balance start, spread, balancer current, SOC 100 % / 0 % voltages, capacity), Temperatures (charge, discharge, MOSFET, heating), and (1.0.0) Signals (buzzer, DRY1, DRY2), Data, Links between cells, Functions, Calibration and commands.

**Details worth knowing:**
- **Capacity:** any write of the capacity, even the same value, makes the BMS recompute the remaining charge from the cell voltages (on a test battery 100 → 78 %). FlatJack refuses a write that doesn't change it; a real change still resets SOC.
- **RFV time** is shown but not writable: the BMS stores only RCV time in that register.
- **Not offered on purpose:** emergency time (writing it, even the same value, started emergency mode), the cell count, the settings password (shown on request, changed in the JK app), the port protocol switch (it would cut the link).
- **Switches** (charge, discharge, balancing) at the top of the tab act at once. Charge off sends the charger to Hold.
- **(1.0.0) Functions:** heating, temperature sensors off (with a warning), display always on, smart sleep, PCL off, timed data logging, dry contact pulsing, discharge OCP 2. Float mode is writable here and in Charge.
- **(1.0.0) Signals:** what turns on the BMS's buzzer and its two dry contacts (DRY1, DRY2): one of 15 sources (cell over/under-voltage, temperatures, SOC, current, …) with a threshold and a release value, written in the source's unit: °C for temperatures, % for SOC, mV, mA.
- **(1.0.0) Links between cells:** the resistance of each busbar between cells, in mΩ, which the BMS uses to correct cell voltages under current.
- Over **Bluetooth** settings are read only; writes need the cable. With the JK app open over Bluetooth the cable link can be disturbed for minutes (Hold, then charging resumes).

## Calibration and BMS commands (1.0.0)

At the end of the BMS tab. Over the cable only. Each asks for confirmation.
- **Voltage calibration:** type the battery's real voltage measured with an accurate voltmeter at the BMS. Accepted within 2 % of the BMS's reading, because the charger regulates on this voltmeter.
- **Current calibration:** type the real current measured with a clamp meter: 0 while the BMS reads at most 0.2 A (sets the zero), or a charge current of 5 A or more within 20 % of the BMS's reading.
- **Set the BMS clock** from the controller's time (needs internet time).
- **Restart the BMS:** the BMS switches discharge off for about 5 seconds while it restarts. With the mains on the Flatpack keeps the house fed; without it the house loses power for those seconds.

## Alarms

The BMS's alarm bits are shown by name: on the screen the first in the top bar (red; not the BMS's reminder to change its password, a note on the web page) and all of them when you tap the bar (1.4.0), on the web page in the battery's alarm list, in Home Assistant as a text. Among them: cell over/under-voltage, charge/discharge overcurrent, short circuit, temperatures (charge, discharge, MOSFET, too cold), cell spread, wire resistance, cell count, current sensor, (1.0.0) temperature sensor fault, current limiter, short circuit not cleared, discharge overcurrent 2 / 3, too cold to discharge, GPS lock, and the BMS's user alarms (heater, charger link, relays, temperatures; on the screen only in the list the bar opens).

## How long the battery lasts

"Enough for" / "Lasts without mains" on the screen and the web page.
- **Energy left:** the capacity left × the battery's voltage (at most 3.2 V a cell, LiFePO4's average), down to the BMS's 0 %. An inverter that cuts off earlier makes it optimistic by that much.
- **The house load** = Flatpack power − battery power, so it is known with the mains on too (the inverter runs from the 48 V).
- **What it learns:** the last minutes' load, a profile of 48 half-hours of your day (learned over about a week of mains-on use), and how the house uses power during outages compared with that profile. A load the profile can't explain (a heater switched on to stay) is taken as lasting.
- Over a week shows "7+ days". A first day without a profile may be off.

## Energy (1.2.0)

Under the history on the overview, **Energy** counts kWh: today, this month and in total, plus bars by day or by month. On the screen: **History → Energy** (1.4.0), the last seven days.
- **Flatpack gave**: its DC output, V × I of every status frame (5 a second). Of it, **From the generator** while the power limit is on.
- **From the mains ≈**: an estimate, output ÷ 0.95. The Flatpack reports no input current, so the mains side is not measured.
- **Into the battery** / **From the battery**: V × I of the BMS, once a second.
- **Load** = Flatpack − into the battery + from the battery (the inverter runs from the 48 V bus).

The counters are saved every 10 minutes, so a power cut loses at most that. Finished days are kept for years. The first start of this version adds the history's last 30 days. If over a day the Flatpack's count differs from a meter you trust, set **Flatpack current correction**: new = current × real kWh ÷ shown (0.8–1.2). Home Assistant gets five energy sensors for its Energy dashboard. (1.4.1) Before 1.4.1 a mains outage could add hundreds of kWh (the Flatpack's current was read wrongly), so 1.4.1 builds the counters and the days once more from the history (its 30 days; older days go): Home Assistant sees that as one meter reset.

## Charge history

Every 2 minutes: voltage, battery current, Flatpack current, SOC, charger phase, temperatures (battery, MOSFET, Flatpack) and cell spread, kept for 30 days on the board (a power cut loses at most 2 minutes). The web chart shows 2 h, 6 h, 1, 3, 7 or 30 days with a crosshair (mouse, finger or arrow keys) and **Download CSV**. The coloured strip on top is the charger's phase. A break in a line: the controller was off or the BMS silent. The history needs internet time (NTP). On the screen: **History → Day / Week** (1.4.0): charge %, battery power and voltage.

## Bluetooth

The board can reach a JK-PB BMS over Bluetooth, through the BMS's own module (the one the JK phone app uses). Both boards have it; the ESP32 DevKit since 1.2.0, where a firmware upload over Wi-Fi switches Bluetooth off and the board restarts afterwards.
- **Pairing:** **System → Bluetooth → Find a BMS nearby → Add**, or on the screen **Settings → Connection → Bluetooth → Find a BMS → Add** (1.4.0). Up to 3. Add a BMS while its cable answers: otherwise FlatJack can't tell which wired battery it is. Close the JK app first: a BMS takes one Bluetooth connection at a time.
- **A spare for the cable:** while the cable answers, Bluetooth stays off. If the cable is silent for 5 s, FlatJack connects over Bluetooth and keeps charging from it; once the cable has answered again for 30 s, Bluetooth is let go. *New: this switch-over has not been tested on a board yet.*
- **A battery without a cable** works over Bluetooth alone (tested: read, charged to Full, reconnects by itself after restarts).
- **Read only** over Bluetooth: switches and settings need the cable.
- While FlatJack is connected to a BMS, the JK app can't connect to it. With a working cable Bluetooth is off, so the app works then.
- **Forget** on a battery that has no cable removes that battery too.

## Home Assistant

FlatJack announces itself over MQTT (Home Assistant 2024.12 or newer):
1. Install an MQTT broker (the Mosquitto add-on) and the MQTT integration.
2. On the web page, **System → Home Assistant (MQTT)**: the broker as `IP` or `IP:port`, its user and password, **Save**.
3. The device **FlatJack** appears with the battery (SOC, voltage, current, power, capacity, every cell, temperatures, switches, alarms), the Flatpack (voltage, current, power, mains, temperatures, status), the house load, the charger phase, and controls: automatic charging, battery current, the charge limit and the Flatpack power limit. With several batteries each also has its own device "FlatJack battery N".

Names follow the device's language. Values go unavailable while their source is silent, so automations never act on stale data. Topics: `flatjack/<id>/state` (every 5 s), `flatjack/<id>/status`, `flatjack/<id>/set/auto|i_max|soc_max|p_max`. Energy (1.2.0): Flatpack, generator, into and from the battery, load, kWh, `total_increasing`, ready for the Energy dashboard. BMS switches are deliberately not in Home Assistant.

## ESPHome

FlatJack is its own firmware, not an ESPHome configuration, and Home Assistant needs no ESPHome for it: it talks MQTT (above).

- **An ESPHome node already reading the BMS over RS485** (for example `jk_bms` / a Modbus config): take it off the RS485-2 bus, or the two will talk over each other. On Modbus only one device may ask (the master), and FlatJack is that master. Everything such a node showed, FlatJack shows too, and it can change the settings.
- **An ESPHome node reading the BMS over Bluetooth** (`jk_bms_ble`): a BMS takes one Bluetooth connection at a time, so it and FlatJack's Bluetooth can't both connect to the same BMS. Over the cable FlatJack doesn't need Bluetooth, so the two can live together as long as you don't pair that BMS in FlatJack.
- **The Flatpack:** no other device may control it over CAN at the same time (an ESPHome or other Flatpack controller): two controllers would fight over its voltage.
- FlatJack's knowledge of the JK protocol comes partly from the ESPHome community's projects: [syssi/esphome-jk-bms](https://github.com/syssi/esphome-jk-bms) (Modbus register map, the Bluetooth protocol) and [thebitrock/growatt-and-jkbms](https://github.com/thebitrock/growatt-and-jkbms); the Flatpack2 CAN protocol from [the6p4c/Flatpack2](https://github.com/the6p4c/Flatpack2). Thanks to their authors.

## Updates and restarts

- **From the screen:** Settings → the download button beside the version: shows the new version's notes, **Update** installs it (about a minute, needs internet). Nothing installs by itself. While the file is written the screen may flicker with stripes: that is normal and ends with the restart.
- **From the web page:** System → Firmware update → the `…-waveshare-s3.bin` file (not `-full`).
- Settings, Wi-Fi, the history and the paired Bluetooth devices are kept.
- After a restart the Flatpack is logged in again at once, so it keeps its setting through an update; auto charging starts again from Charging.

## Safety and limits

- The Flatpack is kept within 43.2–58 V and 62.5 A; OVP never below the voltage.
- Protection is the BMS's: FlatJack doesn't override temperature or voltage protection, it only stops charging (Hold) when something looks wrong.
- No ground between the board and the battery or Flatpack: only A/B, CAN H/L, and power through an isolated DC-DC.
- The web page has no password: keep the board on your home network.

## Troubleshooting

| Problem | What to check |
|---|---|
| "Looking for battery…" stays | Swap `485_A` / `485_B`. The cable in an **RS485-2** socket (not the one next to CAN). DIP address 1–15. In the JK app, UART1 protocol 001 (JK BMS RS485 Modbus). |
| Battery found, then "No link" now and then | The JK app connected over Bluetooth can disturb the cable link: close it. Check the cable's contacts. |
| No Flatpack | Swap `CAN_H` / `CAN_L`. A 120 Ω terminator at each end of the CAN cable (the board's switch, a resistor at the Flatpack). The Flatpack powered. |
| Charging doesn't start in Auto | The Charge tab says why: BMS charge switch off, settings differ between batteries, a battery silent, settings outside the Flatpack's 43.2–58 V. |
| "Full" while SOC shows 95 % | Normal: Full is the phase. Charging starts again at 90 % after the float time. |
| SOC jumped to 100 % early | The BMS does that at «SOC 100 % at voltage». With the BMS leading, switch on **Two-stage charge** on the Charge tab (1.3.0): FlatJack then keeps below that voltage until the current falls. Check that setting is a bit under RCV. |
| The house lost power during a BMS restart | Expected without mains: the BMS switches discharge off for about 5 s. |
| flatjack.local doesn't open | Use the address from the screen's settings tab or your router. |
| A white frame round the screen | Board revision 1.1 fault: keep **Backlight off too** off. |

## All screens

Every state of the on-board screen, as the demo mode shows it (numbers are made up).

| | | |
|---|---|---|
| <img src="docs/img/manual/en/screen-home-a.png" width="300"><br>Charging | <img src="docs/img/manual/en/screen-home-b.png" width="300"><br>Mains outage: on battery | <img src="docs/img/manual/en/screen-home-c.png" width="300"><br>Topping up, nearly full |
| <img src="docs/img/manual/en/screen-home-d.png" width="300"><br>At the SOC limit | <img src="docs/img/manual/en/screen-home-e.png" width="300"><br>Hold | <img src="docs/img/manual/en/screen-home-f.png" width="300"><br>No battery: the Flatpack alone |
| <img src="docs/img/manual/en/screen-home-g.png" width="300"><br>A battery alarm | <img src="docs/img/manual/en/screen-home-h.png" width="300"><br>Manual mode | <img src="docs/img/manual/en/screen-home-i.png" width="300"><br>Two batteries |
| <img src="docs/img/manual/en/screen-home-j.png" width="300"><br>The widest numbers | <img src="docs/img/manual/en/screen-home-k.png" width="300"><br>Nearly empty, Flatpack silent | <img src="docs/img/manual/en/screen-home-l.png" width="300"><br>Battery unplugged, manual |
| <img src="docs/img/manual/en/screen-home-m.png" width="300"><br>Battery unplugged, still in Auto | <img src="docs/img/manual/en/screen-home-n.png" width="300"><br>On a generator | <img src="docs/img/manual/en/screen-home-o.png" width="300"><br>Discharge switched off |
| <img src="docs/img/manual/en/screen-home-p.png" width="300"><br>Flatpack fan fault | <img src="docs/img/manual/en/screen-home-q.png" width="300"><br>Three alarms, balancing | <img src="docs/img/manual/en/screen-home-r.png" width="300"><br>Mains and battery both feed the house |
| <img src="docs/img/manual/en/screen-home-s.png" width="300"><br>Mode Off | <img src="docs/img/manual/en/screen-home-t.png" width="300"><br>Mode Keep | <img src="docs/img/manual/en/screen-home-u.png" width="300"><br>Charge and discharge off |
| <img src="docs/img/manual/en/screen-home-v.png" width="300"><br>Topping up, nothing flows | <img src="docs/img/manual/en/screen-home-w.png" width="300"><br>BMS over Bluetooth (icon top right) | <img src="docs/img/manual/en/screen-home-x.png" width="300"><br>Several alarms; the Flatpack in alarm |
| <img src="docs/img/manual/en/screen-bat-a.png" width="300"><br>Battery: general | <img src="docs/img/manual/en/screen-bat-i.png" width="300"><br>Two batteries: the «1 of 2» chip | <img src="docs/img/manual/en/screen-bat-j.png" width="300"><br>The widest numbers |
| <img src="docs/img/manual/en/screen-bat-o.png" width="300"><br>Discharge off | <img src="docs/img/manual/en/screen-bat-q.png" width="300"><br>Alarms and balancing | <img src="docs/img/manual/en/screen-bat-u.png" width="300"><br>Charge and discharge off |
| <img src="docs/img/manual/en/screen-cells-a.png" width="300"><br>Cells | <img src="docs/img/manual/en/screen-cells-i1.png" width="300"><br>32 cells: 17–32 | <img src="docs/img/manual/en/screen-cells-i2.png" width="300"><br>32 cells: 1–16 |
| <img src="docs/img/manual/en/screen-cells-q.png" width="300"><br>Cells with alarms | <img src="docs/img/manual/en/screen-sw-a.png" width="300"><br>Battery: switches | <img src="docs/img/manual/en/screen-sw-u.png" width="300"><br>Switches: charge and discharge off |
| <img src="docs/img/manual/en/screen-dlg-sw3.png" width="300"><br>Asking before discharge goes off | <img src="docs/img/manual/en/screen-hweek-a.png" width="300"><br>History: a week | <img src="docs/img/manual/en/screen-energy-a.png" width="300"><br>Energy by day |
| <img src="docs/img/manual/en/screen-energy-n.png" width="300"><br>Energy with a generator | <img src="docs/img/manual/en/screen-charge-a.png" width="300"><br>Auto | <img src="docs/img/manual/en/screen-charge-e.png" width="300"><br>Hold: the reason in the footer |
| <img src="docs/img/manual/en/screen-charge-f.png" width="300"><br>Manual without a battery | <img src="docs/img/manual/en/screen-charge-h.png" width="300"><br>Manual | <img src="docs/img/manual/en/screen-charge-j.png" width="300"><br>The widest numbers |
| <img src="docs/img/manual/en/screen-charge-l.png" width="300"><br>Battery unplugged, manual | <img src="docs/img/manual/en/screen-charge-m.png" width="300"><br>No battery: manual mode only | <img src="docs/img/manual/en/screen-charge-n.png" width="300"><br>Generator on |
| <img src="docs/img/manual/en/screen-charge-s.png" width="300"><br>Off | <img src="docs/img/manual/en/screen-charge-t.png" width="300"><br>Keep | <img src="docs/img/manual/en/screen-sh-stages-a.png" width="300"><br>Charge stages (tap the footer) |
| <img src="docs/img/manual/en/screen-sh-stages-e.png" width="300"><br>Charge stages in a pause, with its reason | <img src="docs/img/manual/en/screen-sh-alarms-x.png" width="300"><br>All alarms (tap the top bar) | <img src="docs/img/manual/en/screen-sh-psu-a.png" width="300"><br>Flatpack (tap its card) |
| <img src="docs/img/manual/en/screen-sh-psu-b.png" width="300"><br>Flatpack silent | <img src="docs/img/manual/en/screen-set-a.png" width="300"><br>Settings | <img src="docs/img/manual/en/screen-set-sleep.png" width="300"><br>Screen off after 30 min |
| <img src="docs/img/manual/en/screen-set-f.png" width="300"><br>While the setup network is open | <img src="docs/img/manual/en/screen-sh-ble-a.png" width="300"><br>Bluetooth: one paired, two found | <img src="docs/img/manual/en/screen-sh-ble-x.png" width="300"><br>Bluetooth: connecting, not answering, on standby |
| <img src="docs/img/manual/en/screen-dlg-mode.png" width="300"><br>Asking before a mode change | <img src="docs/img/manual/en/screen-dlg-qr.png" width="300"><br>QR code for the phone | <img src="docs/img/manual/en/screen-dlg-wifi.png" width="300"><br>Change Wi-Fi? |
| <img src="docs/img/manual/en/screen-upd-checking.png" width="300"><br>Update: looking | <img src="docs/img/manual/en/screen-upd-current.png" width="300"><br>Update: newest already | <img src="docs/img/manual/en/screen-upd-new.png" width="300"><br>Update: a new version |
| <img src="docs/img/manual/en/screen-upd-loading.png" width="300"><br>Update: writing | <img src="docs/img/manual/en/screen-upd-done.png" width="300"><br>Update: done, restarting | <img src="docs/img/manual/en/screen-upd-failed.png" width="300"><br>Update: failed |

## For the technically minded: the web API

JSON over HTTP, no password; POST needs `Content-Type: application/json`. `b` is the battery number from 0.

| Method | Path | What |
|---|---|---|
| GET | `/api/state` | Everything as JSON (also pushed on WebSocket `/ws` every 500 ms) |
| GET | `/api/history?from=<unix s>` | History, 16-byte samples |
| POST | `/api/charger` | `{mode: off/keep/auto/manual, i_max, soc_max, two_stage}` (`two_stage` 1.3.0) |
| POST | `/api/psu/set` | `{v, i, ovp}`, manual mode only |
| POST | `/api/psu/power` | `{p_max}` W, 0 = none, else 100–4000 |
| POST | `/api/bms/switch` | `{b, name: charge/discharge/balance, on}` |
| POST | `/api/bms/set` | `{b, key, value}` one setting |
| POST | `/api/bms/cmd` | `{b, cmd: cal_v/cal_i/clock/restart, value}` (1.0.0) |
| POST | `/api/bms/forget` | `{b}` |
| GET / POST | `/api/mqtt` | `{host, user, pass}` |
| POST | `/api/lang` | `{lang: uk/en/ru}` |
| GET / POST | `/api/ota` | the on-board update: `{do: check/install}` |
| GET / POST | `/api/ble` | Bluetooth: `{do: "scan"}`, `{add: mac, type, name}`, `{remove: k}` |
| POST | `/api/update` | firmware file, multipart |
