# Module `Simulation`


**_NOTE:_**

There are separate versions of the simulation module for the *qt* and *pygame* GUIs of BlueSky. This document **only discusses the *qt* version** of the sim module.

---

## Class Simulation 

- This class is in `simulation.py`

- It is a derived class. Its base class is `QObject`. Therefore it
  inherits many methods that are not visible in `simulation.py`

- It can be used to create a sim object, which in turn contains other
  objects (such as the traf and stack and scnreenio).

#### `__init__(self, navdb)`

Goal: Initializes the simulation object. The simulation object contains
variables to control the simulation, like simt (simulation time), as
well as objects, like traf and stack. Therefore, the simulation object
can easily 'communicate' with the methods/functions of other classes
such as Traffic and CommandStack.

Inputs:

1.  `navdb` - object, instance of the `Navdatabase` class

Ouputs: -

#### `moveToThread(self, target_thread)`

Goal: In BlueSky, the simulation and the gui are on separate threads.
This function specifies to which thread different parts of BlueSky
should be moved to. It makes a call to the `moveToThread` method of the
base `QObject` class. **Best not to modify this function if you don't know
anything about multi-threaded programs!**

Inputs:

-  `target_thread` - object, instance of the `Thread` class

Ouputs: -

### `eventTarget(self)`

**<span class="mark">TO BE WRITTEN</span>**

### `doWork(self)`

Goal: This is the main method of the `Simulation` Class. It calls methods from `CommandStack` and `Traffic` classes (amongst other classes) in a while loop until the simulation is quit. The methods of the other classes that are called from within the `doWork` function are, for example, responsible for processing all stack commands and updating the states of the traffic. In this sense, this function contains the main simulation loop
(not to be confused with the `MainLoop` function in `BlueSky_qtgl.py`).

Inputs: -

Outputs: -

### `stop(self)`

Goal: As the name suggests, this function is called to stop the
simulation. It changes the mode of the simulation to 'end' (or `mode==4`)
and asks the `screenio` object to stop the visualization.

Inputs: -

Outputs: -

### `start(self)`

Goal: As the name suggests, this function is called to start the simulation. It changes the mode of the simulation to 'op' (or `mode==1`).
It is called from several places, including the `doWork` function of the
`Simulation` class (see above), and by various BlueSky commands when they
are processed by the `process` function in the `CommandStack` class.

Inputs: -

Outputs: -

### `pause(self)`

Goal: As the name suggests, this function is called to pause simulation. It changes the mode of the simulation to 'op' (or `mode==2` ). It is called
when the *hold* BlueSky command is processed by the `process` function in the `CommandStack` class.

Inputs: -

Outputs: -

### `reset(self)`

Goal: As the name suggests, this function is called to reset simulation.
It changes the mode of the simulation to 'init' (or `mode==0`). It is
called when the *IC* BlueSky command is processed by the `process`
function in the `CommandStack` class to load a new scenario file. It also
resets the simulation time (`simt`) to 0 and resets the traffic arrays by
calling the `traf.reset()` function in the `Traffic` class.

Inputs: -

Outputs: -

### `fastforward(self)`

Goal: As the name suggests, this function is used to speed up the
simulation, i.e., a Fast Time simulation. It is called when the *FF*
BlueSky command is processed by the *process* function in the
CommandStack class.

Inputs: -

Outputs: -

### `datafeed(self,flag)` 

Goal: This function activates the feeding of external data to blueSky,
such as from an ADSB antenna. It is called when the *DATAFEED* BlueSky
command is processed by the *process* function in the CommandStack
class.

Inputs:

-  `flag` (string, 'ON' or 'OFF' to turn on or off the data-feed).

Outputs: -

## Class `Thread`

- This class is in thread.py

- It is a derived class. Its base class is `QObject`. Therefore it
  inherits many methods that are not visible in `thread.py`

### `__init__(self, worker)`

Goal: Initialize an instance of the Thread class, making use the init
function of the base `QObject` class. It also 'connects' the `doWork`
method of the 'worker_object' to the simulation thread.

Inputs:

1.  `worker` :- `object`, in the case of BlueSky, the worker_object is an
    instance of the `Simulation` class)

Outputs: -

## `start(self, prio)`

Goal: As the name suggests, this method starts a simulation thread with
the desired priority,

Inputs:

1.  `prio` :- `int`, the priority of the thread that is being started -\> for
    the sim thread, the highest priority is used)

Outputs: -

## `quit(self)`

**<span class="mark">TO BE WRITTEN</span>**

## Class `ThreadManager`

- This class is in `screenio.py`

- It is a derived class. Its base class is `QObject`.

- To do with running multiple scenarios at the same time

- **<span class="mark">TO BE WRITTEN</span>**

### `instance()`

**<span class="mark">TO BE WRITTEN</span>**

### `currentThreadIsActive()`

**<span class="mark">TO BE WRITTEN</span>**

### `__init__(self, parent=None)`

**<span class="mark">TO BE WRITTEN</span>**

### `getSenderID(self)`

**<span class="mark">TO BE WRITTEN</span>**

### `setActiveNode (self, nodeid)`

**<span class="mark">TO BE WRITTEN</span>**

### `startThread(self, worker_object, prio=Thread.HighestPriority)`

**<span class="mark">TO BE WRITTEN</span>**

## Class `ScreenIO`

- This class is in `screenio.py`

- It is a derived class. Its base class is `QObject`.

- This class acts as the interface between the Gui Class and the
  `Simulation` Class, and allows the `sim` object to send/receive data
  to/from the gui object.

- To this end, it contains many methods (slots and functions). ~~These
  are not discussed below as the average user of BlueSky is unlikely to
  modify the GUI.~~

- The function `objappend` can be used to draw simple shapes (such as experiment areas) on the radar widget. Currently it is set up to draw squares and circles (used for defining experiment areas). It can also be used to draw abstract shaped (experiment areas) objects and simple lines.

**<span class="mark">TO BE WRITTEN</span>**

## Classes in `simevents.py` 

- Definition of data content to be transferred between GUI and Sim
  ~~tasks~~ Classes

- These definitions are used on both sides of the communication

- There are many small classes in this script which derived from the
  *QEvent* base class.

- *It looks like some kind of state-machine setup?*

- Due to small size of the classes in this script, all these classes are
  described in this chapter

## Class SimStateEvent

**<span class="mark">TO BE WRITTEN</span>**

## Class DisplayFlagEvent

**<span class="mark">TO BE WRITTEN</span>**

## Class SimInfoEvent

**<span class="mark">TO BE WRITTEN</span>**

## Class StackTextEvent

**<span class="mark">TO BE WRITTEN</span>**

## Class ShowDialogEvent

**<span class="mark">TO BE WRITTEN</span>**

## Class RouteDataEvent

**<span class="mark">TO BE WRITTEN</span>**

## Class DisplayShapeEvent

**<span class="mark">TO BE WRITTEN</span>**

## Class ACDataEvent

**<span class="mark">TO BE WRITTEN</span>**

## Class AMANEvent

**<span class="mark">TO BE WRITTEN</span>**

## Class PanZoomEvent

**<span class="mark">TO BE WRITTEN</span>**

## Class SimQuitEvent

**<span class="mark">TO BE WRITTEN</span>**

## class `SimulationManager`

- This class is in `simmanager.py`

- It is a derived class. Its base class is `ThreadManager` (see above)

### `__init__(self, navdb, parent=None)`

**<span class="mark">TO BE WRITTEN</span>**

### `addNode(self)`

**<span class="mark">TO BE WRITTEN</span>**

### `stop(self)`

**<span class="mark">TO BE WRITTEN</span>**

### `getSimObjectList(self)`

**<span class="mark">TO BE WRITTEN</span>**

### `getActiveSimTarget(self)`

**<span class="mark">TO BE WRITTEN</span>**

### `event(self, event)`

**<span class="mark">TO BE WRITTEN</span>**
