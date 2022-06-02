# Design and Fabrication of Lasercut Tubes

## Design of Tubes
Lasercut tube designs can be designed in 3D (Solidworks) or 2D (MATLAB or AutoCAD).
Ultimately, you will need an unwrapped version of the design if we fabricate in-house.
We collaborate with outsourced manufacturing firms: Pulse Systems, Illumina, and MDI.
Pulse will sometimes unwrap the design for us, but the others require an unwrapped design.
Designs should be saved as .DXF extension.

## Fabrication of Design using SFLaser Engraver (100W)
1. Disengage the ESTOP button by twisting, and turn on laser key switch - the unit should come on and fans should run.
2. Remove the shutter from the laser head.
3. Place a rectangle the diameter of the tube on the document. (OD width x 15mm long)
4. Place the tube stock in the rotary chuck and lightly tighten down. Use the tailstock if the tube is long and needs a second support. A mandrel should be placed inside of the portion of the tube that is to be cut (steel rod stock).
5. Click on 'LIGHT' in the cartesian axes mode (default). The rectangle should show up continuously. Try to align the tube with the rectangle light such as to block out any projection of the light under the tube. After alignment is complete, deselect 'LIGHT' to stop the rastering of the light.
6. Set laser settings: **TODO: add screenshot of nominal settings**
7. **The laser must be focused for the given diameter of the tube used.** To perform laser focusing, put up the laser curtain and alert anyone working in the fabrication area that laser light will be emitted during this step and the cabinet will be open. The crank wheel on the top of the laser is used to raise and lower the laser head, adjusting the focus. Per the datasheet, the laser is in focus when the sound of the laser cutting is most audible.
8. Place a line to cut on the tube in the document. With the laser curtain up and laser safety glasses on, press 'MARK' in the cartesian mode and adjust the focus crank wheel until the laser sounds the loudest when cutting. You can re-run the job multiple times, but note that the material is being removed and therefore the focus point changes.
9. After the laser is focused, place your design, centered vertically on the vertical axis of the document. **TODO: add screenshot**
10. Go to the ```> Laser > RotaryMark``` tab to open the rotary marking window.
11. **TODO: add screenshot of this window**
12. 
