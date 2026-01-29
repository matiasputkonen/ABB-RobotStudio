# ABB RobotStudio Station – Pick & Place with Smart Gripper

## Description

Tutorial station demonstrating a basic pick & place workflow using ABB RobotStudio,
RAPID programming, and a Smart Component–based gripper with attach/detach logic.

The station focuses on correct separation of:
- RAPID logic (motion + I/O)
- Smart Component logic (physical attachment of parts)

---

## Contains

- ABB industrial robot (IRB series)
- Smart Component gripper (SC_Gripper)
  - Jaw open / close
  - Attach & Detach logic
- One movable workpiece (Part_3)
- Defined workobject and targets
- RAPID program with:
  - Pick routine (`haku`)
  - Place routine (`vie`)
  - Main sequence

---

## Functionality

- Robot moves to approach and pick position
- Gripper closes using DO signal
- Part is attached to the gripper via Smart Component `Attacher`
- Robot moves to place position
- Gripper opens and part is detached
- Robot returns to approach / home position

Attachment is handled **inside the Smart Component**, not in RAPID.

---

## Signals Used

### Digital Outputs (Controller → SC_Gripper)
- `DO_Digital_close` – Close gripper
- `DO_Digital_open` – Open gripper

### Digital Inputs (SC_Gripper → Controller)
- `DI_GripperClose` – Gripper closed feedback
- `DI_GripperOpen` – Gripper open feedback
- `DO_PartAttached` – Part attached status

---

## RAPID Structure

- `PROC haku()`
  - Move to pick
  - Close gripper
  - Wait for closed signal
  - Lift part

- `PROC vie()`
  - Move to place
  - Open gripper
  - Wait for open signal
  - Release part

- `PROC main()`
  - Calls `haku`
  - Calls `vie`

---

## Smart Component Logic

The gripper Smart Component contains:
- `Attacher`
  - Attach on `DI_GripperClose`
  - Attach nearest part
- `Detacher`
  - Detach on `DI_GripperOpen`

This ensures the part physically follows the robot during motion.

---

## Open the Station

Open the station in RobotStudio via:

**RobotStudio → File → Open → Pack & Go**

---

## Notes

- The part must not be fixed or grounded
- Attachment will not work without Smart Component logic
- DO/DI signals alone do not move parts

---

## Purpose

This station is intended as a learning example for:
- Smart Component usage
- Proper pick & place modeling
- Separation of RAPID control and physical simulation

