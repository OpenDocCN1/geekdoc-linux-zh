# A Thermostat

Let us move on to something a little more interesting, and potentially even useful. We will enhance the measure program by turning it into a “thermostat.” We will also take a look at using the host workstation as a preliminary testing environment.

We will have our thermostat activate a “cooler” when the temperature rises above a given setpoint, and turn the cooler off when the temperature falls below the setpoint. In practice, real thermostats incorporate hysteresis that prevents the cooler from rapidly switching on and off when the temperature is right at the setpoint. This is implemented in the form of a “deadband,” such that the cooler turns on when the temperature rises above the setpoint + deadband, and does not turn off until the temperature drops below setpoint − deadband. Additionally, the program includes an “alarm” that flashes if the temperature exceeds a specified limit.

Two of the LEDs will serve as the cooler and alarm respectively. These are defined in driver.h in the measure/ directory as COOLER and ALARM. The thermostat itself is fundamentally a simple state machine with three states based on indicated temperature:

+   - Normal
+   - High
+   - Limit

For each state, the action taken and next state are:

Current state Normal
Temperature above setpoint + deadband
Turn on COOLER
Next state = High
Temperature above limit
Turn on ALARM
Next state = Limit
Current state High
Temperature below setpoint − deadband
Turn off COOLER
Next state = Normal
Temperature above limit
Turn on ALARM
Next state = Limit
Current state Limit
Temperature below limit
Turn off ALARM