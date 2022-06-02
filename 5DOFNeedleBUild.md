# How to build a 5DOF Sensorized Needle

A 5DOF needle may refer to a stylet that is usually used as a piercing tool to exit the bronchial airway, or it may refer to an under-sensed steerable needle. Both use the same 5DOF sensor from NDI for the Aurora EM tracking system.

**TODO: add 5DOF sensor number used for ordering**

These sensors come with no connector attached, and not programmed. The sensor is simply a coil of wire wrapped around a ferromagnetic core -- we usually order the smallest sensor possible, which comes in at 0.45mm diameter and 5mm long. This sensor does not provide any information about the roll angle about its axis (i.e. it only provides a vector at some position in 3D space).

To use this as a steerable needle, we need to use a model to predict that roll angle -- unfortunately this happens to be the most difficult and most important orientation angle, as it defines the orientation of the bevel. Using a Kalman filter or other estimation algorithm, we can estimate this angle for a calibrated needle and use that for steering.

## Materials List
- Nitinol tubing with minimum ID: 0.55mm
- 5DOF EM tracking sensors (NDI #)
- SROM chip (NDI)
- SROM file (NDI Support Site - #)
- 4-piece connector housing (NDI #)
- Loctite superglue (McMaster #)
- Toothpick or other applicator for superglue
- Snaking wire for routing sensor wires through tube
- Tygon tubing for sheath material to protect exposed wires
- Soldering iron
- Dissection microscope
- Nice tweezers
- 28 gauge solid core wire
- Razor blade for stripping enamel coating
- Soldering Helping hands
- Electrical/scotch tape

## Fabrication of Needle

## Assembly of Needle and Sensor

## Testing Sensor

## Permanently Programming the SROM Chip
