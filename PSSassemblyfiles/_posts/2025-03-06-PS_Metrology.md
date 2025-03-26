---
title: PS Sandwich Metrology
tags: PS Metrology Smartscope
---

# Introduction 

Metrology is ran to determine and ensure that the modules built are within spec in terms of spacing for further instalation of the hybrids. A failure of the metrology will make the sandwich unusable for the detector.

Run time: `(4 minutes)`{:.info} 

## Preparation 

* Remove 3D printed nuts to expose all 3 inserts 
* Place carrier plate against bracket (2 insert side toward back of Smartscope)

## Running the program 

* Run Smartscope routine 
```java
(PS_Sandwich_Metrology_Carrier.rtn)
```
* When prompted name results in format `PS_XX_BRN-1XXXX_RunX.DAT`{:.warning} and `PS_XX_BRN-1XXXX_RunX.TXT`{:.warning}
* Initial 2 alignment points in routine are the 2 non-insert holes between the 2 inserts.
* Routine will then move to sensor fiducials.  It will take the centroid of the circle in the middle of the L fiducial and then move the circle to where it thinks the circle is.  If centroid was correct just press enter, otherwise move circle to the correct position and then press enter.
* Routine will then take pictures of the scratchpad on the PSS and the arrow on the PSP
* Lastly routine will do a laser scan along edges of CFBP to check for flatness


## Analyze data
* Copy **TXT file** and **BMPs** from Smartscope computer to shared drive 
```java
(S:/Assembly/Metrology/PS/<module_name>)
```
* Go to [colab.google](https://colab.google/) and login with brownhep account
* Open 
```java
PS_Sandwich_Metrology.ipynb
```
* Select **Run all** from the Runtime menu
* Click `Choose Files`{:.info} to upload the  **TXT files** created by the Smartscope
* Scroll to the bottom of the page to see the output (any out of spec measurements will show up in `red`{:.error})

```java
Files to analyze:  ['PS_XX_BRN-1XXXX_RunX.TXT']

Analyzing PS_XX_BRN-1XXXX_RunX.TXT...
Date: 01:23:25 17:03:40 

SANDWICH METROLOGY:

Rotation (< 800 μrad): 99.5 (CCW positive)
Translation perpendicular to strips, x (< 50 μm): 25.8
Translation parallel to strips, y (< 100 μm): 8.0

MODULE METROLOGY

Delta Inserts (um):  [[0.19, -0.014], [0.19, 0]]
Delta PSS (> 100 um check jig, > 200 um module is bad): [43.0, 2.4]
Delta PSP (> 100 um check jig, > 200 um module is bad): [35.0, 23.4]

MODULE:
Dimensions of PSS/PSP and heights from CFBP to PSP and PSS in mm

																							o (dx: 0.19, dy: -0.014)
	0.585 (0.345-0.395)	4.545 (4.495-4.695)	PSS: 98.138 (98.14)	PSP: 98.739 (98.74)	5.034 (4.495-4.695)	1.075 (0.345-0.395)	
	---										---
	PSS: 49.161 (49.16)									PSS: 49.159 (49.16)
	PSP: 49.161 (49.16)									PSP: 49.159 (49.16)
	---										---
	0.556 (0.345-0.395)	4.506 (4.495-4.695)	PSS: 98.138 (98.14)	PSP: 98.74 (98.74)	4.987 (4.495-4.695)	1.034 (0.345-0.395)	
o											<> (dx: 0.19)

y
^
|
o--> x

Generating XML: PS_XX_BRN-1XXXX_RunX.xml

```

## Make entry into local DB

* Enter rotation and x,y offsets into Metrology page in [local DB](https://collider-parts-db.web.app/)
* Attach photos of scratchpad of PSS and verify that number encoded in scratchpad matches scratchpad number shown in local DB
* Upload metrology data into **CMS DB**
XML will be generated and placed on the Brownhep **Google Drive** in 
```java
MyDrive/Assembly/Metrology/XML/<module name>/
```
* Copy the XML file to your Metrology folder in your **lxplus** account using **WinSCP**
* Use PuTTy to ssh into your lxplus account
* Upload to CMS DB and then move XML file to Uploaded folder:

```java
cd Metrology
python3 cmsdbldr_client.py --login2 --url=https://cmsdca.cern.ch/trk_loader/trker/cmsr <xml_name>
mv <xml_name> Uploaded
```
