---
layout: default
title: 3WA / ETU600
autolink: true
---

## 3WA / ETU600

### Rotary switches:
The ETU600's rotary switches override any corresponding parameter set through the onboard display or PowerConfig, unless in the **e.SET** position.  Note that the switches must be set *between* the lines and not on them, otherwise the trip unit will not read the settings correctly. 

### Option Plug:
The option plug (referred to as "rating plug" on 3WL) must be fully seated until it clicks, or it can cause error codes to appear.  Note that care must be taken to avoid bending the pins inside the socket, as this can permanently damage the ETU.  

### ETU600 bench testing outside of breaker:
It is possible to "bench test" an ETU600, however you must have a breaker harness to do so.  At the minimum, the large X21 connector above the voltage tap cradle must be connected, as well as the two smaller black connectors to the TUI600 (USB/Bluetooth) module on the back of the trip unit.  This will allow the trip unit to be powered via the USB port or the 24VDC control power connections.  Depending on how much of the breaker components are connected, you may get several error codes as detailed in the "Error codes and possible fixes" section below. 	

### Power, USB cable, and PC specifics:
If the trip unit needs to be powered via USB, it must have a native USB-C port and the ability to deliver 1.5A at 5VDC.  

To communicate with the trip unit via USB, a PC with a native USB 3.2 "Power Delivery" port with type-C connector must be used, along with a USB-C cable that is capable of delivering both data *and* 1.5A.  For certainty, use a Thunderbolt 4 or 5 compatible cable, as this standard exceeds the requirements ensures that both power and data capability are to the necessary capacity.  I carry a 15W power bank and a Thunderbolt 5 cable and it will reliably power an ETU600.  

### "Stuck in DAS+" (AERMS mode) Troubleshooting:
DAS+/AERMS can only be deactivated by the same method it was activated.  This is a safety lockout to ensure that the breaker is not accidently switched out of DAS+ mode while someone has the equipment open.  DAS+ mode will be indicated by a bright blue LED, 4th from the left, under the F2 button.

DAS+ conditions can be "stacked".  If it is set by multiple sources (i.e., key switch, keypad, COM190, and Bluetooth), ALL of those sources must be toggled off for the trip unit to come out of DAS+ mode.  If a trip unit is not coming out of DAS+ mode, connect it to a PC running the latest version of PowerConfig.  Load the 3WA, go to the "Measurements" page (gauge button), and click "Go Online" (sunglasses button).  Depending on connection, it may take up to a minute for the data to update.  Under Status Values -> Status -> DAS+ enabled from, there should be 15 true/false values.  Any values that show as "true" need to be resolved via that method before the ETU will come out of DAS+ mode.  Some explanations of the types follow:

**ETU display** - DAS+ was activated via the ETU display and keypad.  Go back to the main menu, press the DAS+ softkey, and the option to reset should appear.

**ETU input** - DAS+ was activated via the ETU digital input.  On QT equipment, this should be the key switch.  Turn it to "off".  If it was already off, turn it "on" and see if that changes the value.  If it does, the AERMS is wired improperly.

**COM A/COM B** - DAS+ was activated via COM190 (PROFINET/Modbus TCP) or COM150 (Modbus RTU).  The breaker will need to receive a signal to disable this bit through its comm module to deactivate DAS+.  There is no bypass.

**TUI600** - DAS+ was activated by either USB or Bluetooth.  The firmware does not differentiate between the two, and you should be able to deactivate it through PowerConfig via PC or the mobile app.

### Bluetooth connection tips:
PowerConfig mobile is extremely buggy and will often refuse or fail a connection to the ETU.  If it fails on an incorrect pairing code even though you've entered the correct one, force quit the app and try to reconnect.  I've not found a reliable way to make it work other than trying over and over. 

There are two Bluetooth modes not addressed in the 3WA manual, RO and RW.  RO is "read only", and RW is "read/write".  Changes can only be made in RW mode. Sometimes you have to cycle this to make the TUI600 remember what mode it's in.  

Clearing a connection requires three steps:
1. On the trip unit Bluetooth menu, select "Clear Devices"
2. In PowerConfig mobile, delete the device.
3. In the device's Bluetooth settings, find the "3WA" entry and select "forget this device".

### Battery and indicator: 
The battery indicator has three "bars", but these bars do not actually deplete like most battery operated devices.  The indicator is either "full", indicating a good battery, or "empty", indicating the battery needs replacement.  The battery only powers the internal clock, and is a size ½AA, 3.6V lithium.  Siemens catalogue number 3WA9111-0EE81.

### Trip cause storage and control power considerations:
The last trip cause is held in memory as long as control power is present.  A loss of control power after a trip will cause the unit to fall back on its internal capacitor to store the cause.  This capacitor requires the ETU to have been active for at least two hours prior to the trip, and has approximately 24 hours of discharge time before the trip cause is lost.  Retrieving the trip cause without control power requires a PC connection or a USB power pack capable of delivering 1.5A.
 
The trip unit can only log trips based on what it can detect through the breaker CTs and voltage tap (if equipped).  Trips caused by an undervoltage relay or shunt trip are NOT logged as the trip unit does not "detect" them.

### Trip unit self-test:
1. Close breaker
2. From the ETU status screen, select TEST (check screen, but usually F3)
3. F3 down to "ETU self-test with trip"
4. F4 to select
5. Start with "T" (check screen, but usually F3)
6. ETU will check itself, a check mark will appear next to each step when passed
7. After the last check and a brief pause, the breaker will open and display a TRIP caution, which should be logged as TEST.
8. A failure at any point will stop the test and display a caution or warning as appropriate.

### LED Indicators:
- ACT (Active)
	- Off - ETU not activated
	- Flashing green once per second - ETU active
- AL (Alarm)
	- Off - Current is less than the AL1 setting.
	- Amber - Current in at least one phase exceeds the AL1 setting.
	- Red - Current in at least one phase exceeds I~r~ (Overload protection)
- INFO
	- Off - Unit is operating normally.
	- Yellow - Warning is present in system.
	- Red - Error is present in system.
- DAS+
	- Off - AERMS is not activated.
	- Blue - AERMS is activated.

### Accessories:
- The small black lever to engage the lockout is part of the locking provision lever.  If no cylinders are used, the padlock type is default, 3WA9111-0BA37.
- 3WL shunt trips, closing coils, and charging motors are confirmed interchangeable with 3WA.

### COM 190 Specifics:
- It is a known limitation that the ETU600 cannot process a firmware update via COM 190.  Unfortunately mass firmware updates must be delivered individually, via the USB-C connection, and take about 10 minutes.

### Error codes and possible fixes:
- ERROR OPTION PLUG - Check that option plug is correct for the frame size.  Disconnect control power, remove plug, check for bent pins inside trip unit socket or damage to connector on back of option plug.  Reseat until it clicks into place.  Restore control power and re-check.
- ERROR N-CT - If neutral CT is present, check connection and wiring.  If neutral CT is not present, check for a jumper at X8-9 and X8-10.  If no jumper is present, disconnect control power, connect terminals X8-9 and X8-10 with a jumper or piece of wire, then restore control power and re-check.  If bench testing, locate the wires labeled with these terminal numbers and connect them with something like a Wago connector. 
- ERROR GF-CT - If ground fault CT is present, check connection and wiring.  If ground fault CT is not present, check for a jumper at X8-11 and X8-12.  If no jumper is present, disconnect control power, connect terminals X8-11 and X8-12 with a jumper or piece of wire, then restore control power and re-check.  If bench testing, locate the wires labeled with these terminal numbers and connect them with something like a Wago connector. 
- ERROR CURRENT SENSOR (1/2/3) - Siemens troubleshooting will indicate a failed phase CT.  While these are accessible, they're not offered by Siemens as a field replaceable part.  Note that this error can be caused by a summation error if ground fault sensing is set to "direct" or "dual" when there is no ground fault CT present.  If a GF-CT is not used, set ground fault to "residual" in the protection settings.  If bench testing, connect a set of phase CTs if available.
