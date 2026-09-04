---

---

## 3WA / ETU600

Rotary switches:
> The ETU600's rotary switches override any corresponding parameter set through the onboard display or PowerConfig, unless in the **e.SET** position.

Option Plug:
> The option plug (referred to as "rating plug" on 3WL) must be fully seated until it clicks, or it can cause error codes to appear.  Note that care must be taken to avoid bending the pins inside the socket, as this can permanently damage the ETU.  

Bench testing not possible outside of breaker not possible:
> An ETU600 will NOT power up when disconnected from the ACB, even with an external power source.  

USB cable and PC specifics:
> To communicate with the trip unit via USB, a PC with a native USB 3.2 "Power Delivery" port with type-C connector must be used, along with a USB-C cable that is capable of delivering both data *and* 1.5A.  For certainty, use a Thunderbolt 4 or 5 compatible cable, as this standard exceeds the requirements ensures that both power and data capability are to the necessary capacity.  I carry a 15W power bank and a Thunderbolt 5 cable and it will reliably power an ETU600.  

DAS+ mode (AERMS): 
> DAS+/AERMS can only be deactivated by the same method it was activated.  This is a safety lockout to ensure that the breaker is not accidently switched out of DAS+ mode while someone has the equipment open.  DAS+ mode will be indicated by a bright blue LED, 4th from the left, under the F2 button.

Battery and indicator: 
> The battery indicator has three "bars", but these bars do not actually deplete like most battery operated devices.  The indicator is either "full", indicating a good battery, or "empty", indicating the battery needs replacement.  The battery only powers the internal clock, and is a size ½AA, 3.6V lithium.

Trip cause storage and control power considerations:
> The last trip cause is held in memory as long as control power is present.  A loss of control power after a trip will cause the unit to fall back on its internal capacitor to store the cause.  This capacitor requires the ETU to have been active for at least two hours prior to the trip, and has approximately 24 hours of discharge time before the trip cause is lost.  Retrieving the trip cause without control power requires a PC connection or a USB power pack capable of delivering 1.5A.
> 
> The trip unit can only log trips based on what it can detect through the breaker CTs and voltage tap (if equipped).  Trips caused by an undervoltage relay or shunt trip are NOT logged as the trip unit does not "detect" them.

### Trip unit self-test:
>1. Close breaker
>2. From the ETU status screen, select TEST (check screen, but usually F3)
>3. F3 down to "ETU self-test with trip"
>4. F4 to select
>5. Start with T (check screen, but usually F3)
>6. ETU will check itself, a check mark will appear next to each step when passed
>7. After the last check and a brief pause, the breaker will open and display a TRIP caution, which should be logged as TEST.
>8. A failure at any point will stop the test and display a caution or warning as appropriate.

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


### Error codes and possible fixes:
- ERROR OPTION PLUG - Check that option plug is correct for the frame size.  Disconnect control power, remove plug, check for bent pins inside trip unit socket or damage to connector on back of option plug.  Reseat until it clicks into place.  Restore control power and re-check. 
