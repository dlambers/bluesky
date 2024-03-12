# Aircraft Performance in BlueSky # 

The BlueSky aircraft performance model is based on EUROCONTROL ́s User Manual for the Base of 
Aircraft Data (BADA) Revision 3.12. This leads to a full compatibility with BADA data files.  

For users without a license for BADA, a default aircraft model based on open accessible information 
for the Boeing 747-400 is available. It will be automatically used as aircraft type for all simulated aircraft within BlueSky. As the model is a draft only, it should not be used to draw any conclusion upon.   

## Compatibility to BADA 3.12 ##
 Users with access to BADA may replace the default aircraft model with their BADA data files. The 
path is `> data/Aircraft_Coefficients`. To make use of the models, it is required to spell the aircraft type in the flight plan or the user interface as written in the BADA data files (e.g B744 for the Boeing 747-400, B748 for the Boeing 747-800). If  BlueSky cannot find the according aircraft, it will use the default model instead.  

The BlueSky performance model is validated with three jet and three turboprop aircraft for the BADA 
3.12 revision. The validated models are the A320, B744, F100, D328, DH8C and SB20. They were 
each tested in eight flight phases and compared to BADA reference values. The recorded results include speeds, 
thrust, drag, fuel flow, vertical speed and the energy share factor. The maximum deviation between 
BADA and BlueSky amounts to 0.5% with a mean of 0.00025 and  a standard deviation of 0.0015.   

## Contents of the aircraft performance model  ##
The current version of BlueSky ́s performance model includes 
- calculation of the forces thrust, lift ,drag and weight 
- calculation of the current fuel flow and the according aircraft mass reduction 
- calculation of vertical speed in climb and descent as a function of thrust 
- calculation of thrust as function of vertical speed, if vertical speed is set by the user 
- flight envelope protection for minimum speed, maximum speed, maximum altitude and 
maximum vertical speed. A target value outside the envelope leads the autopilot to set a value 
as close as possible to the user's desire inside the flight envelope  

---
**_Note_**:  BADA does not provide information about thrust or fuel flow during ground operation. The 
BlueSky implementation assumes minimum descent thrust and fuel flow for ground operations.    

---

## Data recording ##
 For data recording, the class `CDatalog` may be called with adding the following code fragments to the 
```python
class CTraffic:  

"""  Traffic class definition    : Traffic data """ 
import CDatalog 
... ... ... 
class Traffic():     def __init__(self):  
 self.log = CDatalog.Datalog() 
... ... ... 
    def update(self, sim, cmd): 
     self.log.write(timestep,str(value)) 
... ... ... 

```
 The resulting data file can be found in the folder `> output`. 