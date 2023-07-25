# Brians-IDEX-Nozzle-Calibration-tool

As I almost finished my Anycubic i3 Mega IDEX mod ([GitHub - Life0fBrian/Anycubic-i3-Mega-IDEX-mod: This mod converts the Anycubic i3 Mega into an IDEX 3D printer.](https://github.com/Life0fBrian/Anycubic-i3-Mega-IDEX-mod)) it was time to research on how to properly calibrate/determine the offsets of the two printheads/nozzles.
Most users seem to print some special patterns and change the offsets until everything is fine but the internet and a kind user from the Klipper discourse suggested using a webcam/camera.

But how to get it done with a camera properly? There is at least one commercial solution consisting of a camera-box and software.
I did not want to pay extra money but use the stuff I have here.
As further research on suitable tools for this task was not successful I used inspiration from the WWW and the rest of my grey matter to write a small HTML-page that can run in a web browser almost everywhere and does not require admin rights under Windows.
The GUI looks like follows:
![tool](https://github.com/Life0fBrian/Brians-IDEX-Nozzle-Calibration-tool/assets/84620081/7baaee45-7333-4f96-82a7-7c21d9b99fdb)

You initially set up everything in the printer.cfg so the kinematic of your IDEX printer is running properly and have your belts tightened and then you just home all axes and move either the print heads upwards (cartesian printer) or the bed downwards (CoreXY) so that a webcam or other camera fits underneath the nozzle with some space to it:
![20230719_145510](https://github.com/Life0fBrian/Brians-IDEX-Nozzle-Calibration-tool/assets/84620081/dae516c0-4bfc-4631-b09e-e52d4d7405d3)

The cameras image plane must be parallel to the bed and the camera somehow fastened to the bed if you need to adjust Y offsets as well.
Z offsets of the nozzles should be corrected before this whole procedure.
The red circle where the nozzle tip has to fit in can be resized to have a better orientation.

Then move T0 to for example X=100 and arrange the camera underneath its nozzle so that it is properly focused/sharp in the camera stream and so that the nozzle tip is congruent with the red circle in the center of the stream.
Maybe you need to adjust camera focus or Z to achieve this.
Then you switch to T1 and move its nozzle tip into the red circle as well via manual adjustments of X and/or Y.
After that procedure you can read the X and maybe Y coordinates and get your offsets compared to the values of T0.
The new calculated X value is represented by the position_endstop and position_max values on my cartesian setup in the DUAL_CARRIAGE section and the Y offset is set via SET_GCODE_OFFSET Y=xx in the T1 macro.
