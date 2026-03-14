# ABB RobotStudio Station -- Pallet Handling with Measurement Cycle

## Description

RobotStudio station demonstrating a pallet-handling workflow with an ABB
industrial robot programmed in RAPID.

The robot picks parts from an **infeed pallet**, processes them through
a **machine station**, optionally performs **measurement**, and places
finished parts onto an **outfeed pallet**.

The station demonstrates:

-   RAPID motion programming
-   pallet matrix handling
-   conditional measurement logic
-   structured robot workcycle design

------------------------------------------------------------------------

## Contains

-   ABB industrial robot (IRB series)
-   Robot tool (Servo / tool0)
-   Workpiece part
-   Two pallet stations
    -   **Infeed pallet:** 4 × 2 matrix\
    -   **Outfeed pallet:** 3 × 3 matrix
-   Machine station
-   Measurement station
-   RAPID program
-   Workobject and robtargets

------------------------------------------------------------------------

## Targets

### Home

-   pHome

### Infeed pallet

-   pInBase
-   pInApproachBase

### Machine station

-   pMachApproach
-   pMachPlace
-   pMachPick
-   pMachWaitOut

### Measurement station

-   pMeasApproach
-   pMeas

### Outfeed pallet

-   pOutBase
-   pOutApproach

------------------------------------------------------------------------

## Functionality

The robot performs the following cycle:

1.  Move to pick approach
2.  Pick part from infeed pallet
3.  Move to machine station
4.  Place part into machine
5.  Wait for machining
6.  Pick part from machine
7.  Every third part goes to measurement
8.  Place finished part on outfeed pallet
9.  Continue until pallet cycle is completed
10. Return robot to home position

------------------------------------------------------------------------

## RAPID Structure

### PROC PickFromInfeed()

Move to pallet approach\
Move to pick position\
GripOn\
Lift part

### PROC PlaceToMachine()

Move to machine approach\
Move to place position\
GripOff\
Retract

### PROC PickFromMachine()

Move to machine approach\
Move to pick position\
GripOn\
Retract

### PROC VisitMeasurement()

Move to measurement approach\
Move to measurement position\
Wait for measurement\
Retract

### PROC PlaceToOutfeed()

Move to pallet approach\
Move to place position\
GripOff\
Retract

### PROC main()

Initialize robot\
Loop through parts\
Pick from infeed pallet\
Place to machine\
Pick from machine\
Measure every third part\
Place to outfeed pallet\
Return to home\
Stop program

------------------------------------------------------------------------

## Pallet Matrix Logic

### Infeed pallet

4 × 2 pallet matrix.

Positions are calculated using:

CalcInfeedPos()

Offsets are calculated relative to:

pInBase

### Outfeed pallet

3 × 3 pallet matrix.

Positions are calculated using:

CalcOutfeedPos()

Offsets are calculated relative to:

pOutBase

------------------------------------------------------------------------

## Measurement Logic

Measurement is executed conditionally using:

IF partCount MOD 3 = 0 THEN\
VisitMeasurement

This ensures every third part is measured.

------------------------------------------------------------------------

## Signals Used

The gripper operation is simulated using RAPID procedures:

GripOn()\
GripOff()

These represent closing and opening the gripper.

------------------------------------------------------------------------

## Open the Station

RobotStudio → File → Open → Pack & Go

Load the `.rspag` package file to run the station.

------------------------------------------------------------------------

## Notes

-   Pallet positions are calculated dynamically using offsets.
-   RAPID code is structured into modular procedures.
-   Measurement logic demonstrates conditional execution.
-   The robot returns to pHome after completing the work cycle.

------------------------------------------------------------------------

## Purpose

This station demonstrates:

-   RAPID program structure
-   pallet matrix programming
-   conditional robot tasks
-   industrial pick--machine--measure--place workflow
-   ABB RobotStudio simulation fundamentals
