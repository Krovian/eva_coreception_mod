# EVA Coreception Mod

EVA carriage mod for the Creativity ELF/ELF PRO and SainSmart Coreception lines of CoreXY 3D printers

![CAD front view](/images/cad01.png)


## Overview

This is a mod for the EVA carriage platform to work on the Creativity ELF/ELF PRO and SainSmart Coreception lines of CoreXY 3D printers. However, the changes have been made in such a way as to try to increase the configurability of the tool head, making it adaptable to a wider range of printers. In particular, it should be trivial to adapt to other CoreXY printers with a "halo" design, similar to the ELF variants, such as the Two Trees Sapphire.

Overall print area on my Coreception, with this mod installed, is X=297mm, Y=294mm. I believe that moving the BL Touch to the middle, under the gantry, would increase the X travel by about 10mm. And filing down the M3 bolt hole on the rear blower fan, to allow the bolt head to sit flush with the fan casing, would give another ~3mm of Y travel on the rear.

Check out the [main EVA documentation site](https://main.eva-3d.page/) for more details on the EVA platform, information on printing and postprocessing parts, etc. Feel free to reach out to me on the ELF/Coreception Facebook group with questions or concerns.


## Files

STL files are under the [`/stl`](/stl) folder. You will need to select the appropriate [Face] mount for your hot end - V6, Dragon, or Mosquito. There is also an unofficial mount for the stock MK8 hot end [here](https://contrib.eva-3d.page/hotends/microswiss-mk8/). Start with one of the `"_mirrored"` hot end mounts if you plan on using the BL Touch on the the ELF/Coreception. If you're using the onofficial MK8 mount linked above, you'll need to mirror it yourself. I highly recommend printing out and test fitting everything *thoroughly* before disassembling your existing hot end and carriage. I also recommend printing out a spare set of parts, especially anything that is near or touching the hot end. It might also be a good idea to buy some new, higher quality belts before installing. My stock belts were pretty low quality and chewed up pretty badly by the zip ties used to secure them to the stock carriage.

There are multiple versions of the Y end stop (`end_stop_y_XXmm_offset.stl`) with a range of offsets, to allow people to find tune their Y=0 (I figure there may be manufacturing variances). On my machine, I ended up with either a 6mm or 7mm offset. They're a quick print, so I would recommend starting with the 6mm-8mm offsets, plus the 13mm as a fallback. Once everything is assembled, you can print additional offsets to fine tune, if your machine isn't in the 6mm-8mm offset range.

NOTE: There is a `[Misc] tension_slider_6mm_M3.stl` and `[Misc] tension_slider_6mm_M3_flipped_teeth.stl` for the belt tensioners on the rear. My Coreception uses the `_flipped_teeth` variant, but I would suggest printing out a pair of each, just in case. If you print the wrong ones, you will need to assemble your new carriage backwards, which will cut your Y travel almost in half until you print out the correct ones (don't ask me how I know this 😕). You may also want to print out extras, as these are a somewhat delicate part and can occasionally split when inserting the M3 nuts.

My CAD document for this mod can be accessed [here](https://cad.onshape.com/documents/8374df57f21afb0afda371e1/v/ab8b5f501b92076e0e46f97f/e/99eb3d22b4d42aecd6cd179c) (you may need to create a free OnShape account).


## Mod Details

Here's a brief rundown of my changes, starting with a visual comparison between this mod and the original.

![comparison to stock](/images/cad02.png)

1. The overall height of the entire carriage was made configurable, and specifically for the ELF/Coreception, the height of the carriage was increased from the default 57mm to 67mm, to allow the hot end to reach down to the print bed without needing to use longer screws or springs to raise the bed.

2. Better configuration of belt size/position/spacing.

    * Belt width is configurable, 6mm or 9mm.
    
    * Left and right belt anchor heights can be configured independently.
    
    * Belt tension sliders in back were changed to use M3 bolts and nuts rather than M5, to allow tension sliders sized for 6mm belts, and also to allow the sliders to be positioned closer to each other, to support the belt geometry on the ELF/Coreception.
    
    * Configured belt offsets to match the stock carriage. Note that this means you may still need to correct the vertical spacing of the idlers on your X gantry. But it also means that if you've already done so, your belt geometry should remain unchanged.

3. Made the carriage depth configurable, and increased the depth to 30mm, from the default 27mm, to fit over the X gantry bar on the ELF/Coreception. I have only modded the top plate for the BMG extruder because that's the extruder I'm using. Honestly, if you're still using the crappy Titan clone that comes with the ELF/Coreception, upgrading to a BMG clone from Trianglelab is one of the best $25 you can spend. However, modding one of the other top plate variants shouldn't be too hard. All that really needs to be done is to mod the top plate depth from the default 27mm to 30m, making sure that the filament path exiting the extruder remains the same.

4. Mirrored versions of all of the current official hot end tool holders (V6, Mosquito, and Dragon) now have mirrored versions to allow putting the BL Touch or other Z probe on the right side of the tool head. While I didn't try using the original configuration, with the probe on the left, it looked like this would cause a problem since the ELF/Coreception home the X axis on the left.

5. A new fan shroud was created that is both lower profile, to fit underneath the halo, and also thicker, to be robust enough for triggering the Y end stop.

6. Mounting holes were added to the shroud for mounting an accelerometer to use Resonance Compensation (A.K.A. Input Shaper) in Klipper. 

7. Zip tie anchor points were added to the front face and both sides of the upper BMG/stepper mount to allow routing wires up and over the gantry, in addition to the existing zip timeouts on the bottom of the carriage. My wires are currently routed underneath the carriage, but I'm considering changing it at some point to route the wires over the top. This would be especially useful for adding a Molex MicroFit connector to allow [easier swapping of tool heads](https://youtu.be/zYscXKBwh0o?t=166).

![X and Y end stops](/images/cad03.png)
![Y end stop location](/images/cad04.png)

8. Added an X end stop mount in the center section of the carriage. This mount has 2 sets of holes for mounting the stock end stop switch, and can be adjusted left or right to adjust the X=0 point.

9. Added a new Y end stop mount to maximize the amount of Y travel. This mount uses the existing Y end stop PCB and mounts using the 3 empty M3 holes in the halo, just behind and to the side of where the existing end stop screws into place. See pictures and CAD screenshots.

![rear view / breakout board mount / VGA cable holder](/images/cad05.png)

10. Mount and cover for the stock breakout board, including a tiedown to keep the VGA cable from flopping around.


## ADXL345 / Accelerometer Mounting Options

There are 3 options for mouting an ADXL345 accelerometer for Input Shaping with Klipper. The image below shows mounting options using the new `shroud_low_profile_alt_adxl.stl` file. The original `shroud_low_profile_41mm.stl` will also work for options 1 and 2. Note that this new `shroud_low_profile_alt_adxl.stl` is designed to use with [this style of "M3 X D5.0 X L4.0" heat set inserts](https://www.aliexpress.com/item/4000232858343.html) from a Voron BOM, rather than hex nuts, to make it easier to repeatedly mount and remove the ADXL345. Longer or shorter inserts may work, as well as other styles, but I can't say for sure.

![ADXL345 Mounting Options](/images/adxl_mounting.jpg)

From left to right:

1. Bottom mount, using the `adxl345_mount4.stl` file, which is  mounted on the front of the shroud using the bottom two holes for the 40 mm hot end fan. This is meant to be a more permanent mounting solution, where you would leave the ADXL345 mounted in place, and simply plug and unplug as needed.

2. Top mount, using either heat set inserts or hex nuts, depending on which verrsion of the shroud you are using. Note that this will position the accelerometer where it would hit the Y end stop, so you would need to print some kind of shield to protect the accelerometer PCB. A better option would be to mount the accelerometer to the bottom of the shroud.

3. Bottom mount, using heat set inserts. Only `shroud_low_profile_alt_adxl.stl` supports this mounting option.


## Photos

![IMG_20210306_174934603.jpg](/images/IMG_20210306_174934603.jpg)
![IMG_20210306_180101041.jpg](/images/IMG_20210306_180101041.jpg)
![IMG_20210306_181520648.jpg](/images/IMG_20210306_181520648.jpg)
![IMG_20210306_181805664.jpg](/images/IMG_20210306_181805664.jpg)
![IMG_20210306_182301766.jpg](/images/IMG_20210306_182301766.jpg)
![IMG_20210306_182312979.jpg](/images/IMG_20210306_182312979.jpg)
