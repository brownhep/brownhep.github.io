---
title: 2S Sandwich Metrology
tags: 2S Metrology Smartscope
---

# Introduction 

Metrology is ran to determine and ensure that the modules built are within spec in terms of spacing for further instalation of the hybrids. A failure of the metrology will make the sandwich unusable for the detector.

One can do a quick metrology, which measures only the sandwich alignment and module thickness `(5-6 minutes)`{:.info} or one can do a full metrology which also measures the bridge positions `(8-9 minutes)`{:.info}.

## Preparation

* Module should be placed onto dedicated metrology carrier plate
* Remove **3D printed standoffs** from long bridges to expose holes in bridges, but leave nuts in place on the stump bridges (full metrology only)
* Place carrier plate against bracket (**HV tails pointing up** and nearest the bracket)

## Running the program

* Run Smartscope routine 
```java
(2S_Sandwich_Metrology_Quick.rtn, 2S_Sandwich_Metrology_Full.rtn)
```
* Routine will move to the 4 alignment needles, align crosshair to needle tip and press enter on the joystick
* When prompted name results in format `2S_18_5_BRN-10001_Full_Run1.TXT`{:.warning}
* Routine will then move to bridges. For long bridges move circle over holes in the bridges and press enter. For stump bridges move crosshair to corner of bridges and press enter (for 5 point modules just press enter when crosshair is in the position of the missing stump bridge)
* Routine will then move to sensor fiducials.  It will take the centroid of the circle in the middle of the **L** fiducial and then move the circle to where it thinks the circle is.  If centroid was correct just press enter, otherwise move circle to the correct position and then press enter.
* Routine will then take pictures `Top_Sensor.BMP`{:.warning} and `Top_Sensor_Rot.BMP`{:.warning}.  If the scratchpads are in the former picture the top sensor is in the **Not Rotated** state.  If the scratchpads are in the _Rot picture, the top sensor is in the **Rotated state**.
* The lens will then move to its max height to allow the module to be flipped to its back side.  Flip the module so the left side is now the right side and press enter.
Repeat the above steps (minus the bridge measurements) on the back side.


## Analyze data

* Copy **TXT file** and **Top_Sensor** and **Bot_Sensor BMPs** from Smartscope computer to shared drive 
```java
(S:/Assembly/Metrology/2S/<module_name>)
```
* Go to [colab.google](https://colab.google/) and login with brownhep account
* Open 
```java
2S_Sandwich_Metrology.ipynb
```
* Select **Run all** from the Runtime menu
* Click `Choose Files`{:.info} to upload the **TXT files** created by the Smartscope
* Scroll to the bottom of the page to see the output (any out of spec measurements will show up in `red`{:.error}).  

```java
Files:  ['2S_18_5_BRN-10001_Full_Run1.TXT'] 

Analyzing 2S_18_5_BRN-10001_Full_Run1.TXT...

BRIDGE and SENSOR POSITIONS:
Offset from nominal position of bridges (0-100 um) and sensors (100-200 um check jig, > 200 um bad) in um

  <> (18.0, 0.0)	--	--	--	--	--	--	o (-6.0, 16.0)
HV
+ (-33.0, 47.0)							  + (-29.0, -62.0)
|		Top (-65.0, 191.0)	Bot (-69.0, 182.0))	  |
+ (-7.0, 31.0)							  + (14.0, -63.0)

  o (0.0, 0.0)	--	--	--	--	--	--	<> (-8.0, 3.0)
Origin

y
^
|
o--> x

SANDWICH METROLOGY:

Rotation (< 800 μrad): 15.6 (CCW positive)
Translation perpendicular to strips, x (< 50 μm): 2.9
Translation perpendicular to strips, y (< 100 μm): 0.5

SANDWICH:
Dimensions of sensors and thickness at the corners in mm

1.968 (1.9-2.1)		TOP: 102.699 (102.7)	BOT: 102.699 (102.7)		1.971 (1.9-2.1)
---											---
TOP: 94.166 (94.183)								TOP: 94.164 (94.183)
BOT: 94.184 (94.183)								BOT: 94.183 (94.183)
---										---
2.005 (1.9-2.1)		TOP: 102.698 (102.7)	BOT: 102.701 (102.7)		1.982 (1.9-2.1)
									HV HV HV


NEEDLE CHECK (Verifies that needle positions from top and bottom align and measurement was good):

Distance top-bottom needle pair  10.07 7.37 11.63 4.8
                   
Generating XML: 2S_18_5_BRN-10001_Full_Run1.xml
```

## Make entry into local DB

* Enter rotation and x,y offsets into Metrology page in [local DB](https://collider-parts-db.web.app/)
* Attach photos of scratchpads for top and bottom sensors and verify that number encoded in scratchpads matches scratchpad number shown in local DB
* Upload metrology data into **CMS DB**
* **XML** will be generated and placed on the **Google Drive** in 
```java
MyDrive/Assembly/Metrology/XML/<module name>/
```
* Copy the XML file to your Metrology folder in your **lxplus** account using **WinSCP**
* Use **PuTTy** to ssh into your lxplus account
* Upload to CMS DB and then move XML file to Uploaded folder:
```java
cd Metrology
python3 cmsdbldr_client.py --login2 --url=https://cmsdca.cern.ch/trk_loader/trker/cmsr <xml_name>
mv <xml_name> Uploaded
```
