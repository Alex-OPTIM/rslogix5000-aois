# Custom RSLogix 5000 AOI (Add-On Instructions)
## Context
This repo includes a list of exported AOIs to L5K:
- DUTY_CYCLE
- BOOLS_2_DINT
- DINT_2_BOOLS

How to import watch [Importing Add On Instruction in RSLogix 5000 (Studio 5000)](https://youtu.be/DInlqYIBAvg)

## DUTY_CYCLE

DESCRIPTION  
This AOI cycles operation of group of "UNIT"s which operate intermittently by number of hours.  
UNIT is a machine or other device (pump, fan, motor, etc.).

MAIN FUNCTION  
Every N hours it switches to next enabled UNIT

PARAMETERS
- I_NoRunSwitch : BOOL - Set to prevent from switching without removing I_RunRequest (it switches to the next UNIT only with new RunRequest)
- I_RunRequest : BOOL - Set to start (or continue) to duty cycle
- I_RuntimeM_SP : DINT - Number of dutycycle minutes (60 = 1 hour, 480 = 8 hours) [1-1440]
- I_UnitEnabled : DINT.X - Set bit to enable a UNIT in the array of 32
- I_UnitRunOverlapMS_SP : DINT - Machine run overlap in ms [ 0 - 59000 ]

- O_CurrentRuntimeS : DINT - Runtime of current UNIT in seconds
- O_CurrentUnitIndex : DINT - Index of currently running UNIT
- O_Enable_F : BOOL - FAULT: ON is when No UNITs have been enabled
- O_RunningUnit : DINT - Get bit of currently running UNIT

DEPENDENCIES
- BOOLS_2_DINT v1.0
- DINT_2_BOOLS v1.0

### Usage
See a picture below. It shows usage as the following:
- Units 0, 1 and 22 are enabled (number 2 is disabled);
- No Run Switch is OFF;
- Run Request is ON;
- Runtime of each machine is 3 minutes;
- Overlap is 2 seconds

![picture](https://github.com/Alex-OPTIM/rslogix5000-aois/raw/master/tests/test-Duty_Cycle_190828.png)

## BOOLS_2_DINT
MAIN FUNCTION  
Converts array of 32 BOOLs to DINT  
![picture](https://github.com/Alex-OPTIM/rslogix5000-aois/raw/master/tests/test-BOOLS_2_DINT.png)

## DINT_2_BOOLS
MAIN FUNCTION  
Converts DINT to array of 32 BOOLs  
![picture](https://github.com/Alex-OPTIM/rslogix5000-aois/raw/master/tests/test-DINT_2_BOOLS.png)

---
## License

This project is licensed under the MIT License - see the [LICENSE](https://github.com/Alex-OPTIM/rslogix5000-aois/blob/master/LICENSE) file for details

## Other links

- [RS Logix 5000 Tag Converter](https://tags.controlx.io) to import into Node-RED 
module [node-red-contrib-cip-ethernet-ip](https://github.com/netsmarttech/node-red-contrib-cip-ethernet-ip)
- The best Node.JS module [node-ethernet-ip](https://github.com/cmseaton42/node-ethernet-ip) 
