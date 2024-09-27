---
title: Alibava HM Sensor Testing
tags: Alibava HM Test CVIV Annealing Irradiation Analysis
cover: /assets/images/cover/Alivaba.jpg
---

# Alibava HM Sensor Testing 

For our irradiation study, two HM diode chips `(C0 and C1)`{:.info} are irradiated and tested using the Alibava set-up in lab 550, which performs a series of tests from `-300V to -900V at 100 volt intervals`{:.warning}. Extra tests are run at voltages `-600V and -800V`{:.warning}. We do not want the voltage to exceed compliance for the half moons before the 800V mark is reached.

----

**Pre-irradiation:** CVIV for diodes, CVIV for strip sensor, and strip tests @20°C  
{:.info}

**Post-irradiation:** 5-step annealing process  
{:.info}

## Installing HMs to the Alibava board

### Materials
* Small flathead screwdriver
* 3D printed brackets
* Ceramic plate
* Left and right HV (high voltage) PCBs with cables installed
* Gloves
* 4 3M screws

* Take the sensors out of the fridge.

## Placing HMs in the Alibava board

* **If the HMs are irradiated**, allow the HMs to warm up to room temperature (~25°C).
* **If the HMs are not irradiated**, take the selected HMs from the dry box.
* Place the ceramic plate in the Alibava chuck.
* Place the **HV PCBs** in the Alibava chuck.
* Insert the 3M screws into the 3D printed pieces and set them aside.
* Carefully take the HMs from their bags and place them on the ceramic plate.
* Align the HMs with the fanboard of the Alibava board.
* Carefully place the 3D printed bottom bracket with screws.
* Screw the 3D printed part.
    * Ensure the HMs stay aligned while screwing in the 3D printed piece.
* Afterward, take the 3D printed top part and screw it to the chuck.
    * Ensure the HMs are aligned.
* Now, the HMs are ready to be wire-bonded to the Alibava board.

**See:** [Alibava wire bonding](https://brownhep.github.io/2023/10/21/Wire_Bonding_HM.html).

## Placing the Alibava board in the chuck

* **If the HMs are irradiated**, remove the chuck (HMs attached to Alibava board) from the freezer and allow it to warm up to room temperature (until no condensation is on the bag containing the chuck).
* Place the chuck into the Alibava, lining up the black line on the chuck to the base of the Alibava stage (move the source to 0.00 in Owisoft to have more space).
* Tighten the screw on the chuck to hold the Alibava board in place.
* Tighten the two screws at the base of the yellow side of the Alibava board.
* The gold pads are the ground for the Alibava board.
* Place the insulation strips (brown) under the long sides of the Alibava board. This helps keep the temperature and dewpoint more consistent and allows us to use only wall air for the test, not nitrogen tanks.
* Attach the **C0 & C1 green wires** to the green wires on the Alibava board.
* Connect the ribbon cable to the Alibava board (very thick grey wire) to supply power to the sensors.
* Unscrew the screw to the left of the ribbon cable, place the yellow/black cable with the ring on the end onto the screw, and then re-screw it in.
    * This is the ground cable for the Alibava high voltage.
* Rest the humidity/temperature sensor wire to the right of the ribbon cable.
* On the bottom right of the Alibava board, loosen the screw holding down the L-shaped clamp, place the temperature sensor of the chuck under that clamp, and tighten.
* Following proper radiation safety procedures, place the radiation source in the source arm hovering over the half moons.
* In LabVIEW, set the temperature to 20°C and set the chiller (Julabo) to 20°C, only once the Alibava board is inside the setup since LabVIEW is very sensitive.

### Placing the Radiation Source
* The radiation source will sit in the metal arm hovering over the half moons.
* First, put on the radiation ring and badge (in the radiation drawer near the freezer).
    * Unlock the cabinet containing the source with the key from the same drawer.
    * Take out the source container from the cabinet, carefully twist off the outer cap, and use that cap to twist off the red lid of the small container inside holding the source. Remove the source using the pliers at the Alibava station and carefully place it in the source arm.
    * Close the lid of the Alibava box and flip over the radiation safety sign to signify that radiation is in use.
    * Put the caps back on the source container and place it back into the cabinet, locking it afterward.
    * Record the date of use of the source on the sheet above the cabinet.

## Using Owisoft

* **Owisoft** is software used to change the position of the source.
* The Alibava test is run on each chip, and during each test, you have to center the source above that chip before running the test.
* When annealing or setting the system to overnight conditions, move the source to **0.000** so it is not sitting over either chip.
    * The starting position, 0.000, is to the right of C1.
    * C1 is usually between **8.000-13.000**, while C0 is usually between **17.000-24.000**.
* To check the location of the source relative to the center of the chip being tested, you can do a practice run in Local mode on the brown Keithley:
    * **Brown Keithley**: Bias voltage.
    * Set to local, hit the operate button, and use the dial to hover over the tenths place of the voltage.
    * Hit the menu button, scroll to factory initiator, hit enter, hit operate, select autorange.
    * Manually increase the voltage to roughly **-400V to -500V**, and then hit the run button in the Alibava GUI.
        * Increasing to -500V will produce a clearer peak and help better determine the location of the source.
        * One strip = roughly 0.1mm, moving 1mm = moving ~7-10 strips.

## Running an Alibava Test

* Move the IV cable to the chip you want to run in the Alibava setup (located in the second compartment of the setup).
* Plug in the power cable to the Alibava.
* Turn on the power supply by entering **F10** and flipping up the switch so that the red light turns on and ramps up to 900V.
    * Only needs to be on when running tests. For everything else, turn off with **F11** and flip the switch down.
* **If the HMs are irradiated**, set the LabVIEW temp to -15°C, turn on the chiller and set it to -18°C, and turn on the wall air, setting its pressure to roughly 15/20psi.
    * Let the temperature of the chuck reach -15°C, and make sure the dew point is at least 1.2°C lower than the chuck temperature. Ideally, the dew point should sit around -18°C.
* **If the HMs are not irradiated**, for calibrating the Alibava with unirradiated sensors, set the chiller to 15°C and LabVIEW to 20°C, with the Peltiers set to heating.
* In Owisoft, set the radiation source location to be centered over the chip being tested.
* Open **Alibava GUI**.
    * Hit file, open, and select the irradiation study file.
* Open **PuTTY** and log into your Brux account.
    * **Brux** communicates with the **Alibava GUI**, telling it which chip is being tested, where to save the information, the run parameters, and when to start the run.

        ```java
        cd Alibava
        cd Soap
        nano SOAP_HVScan_HiStatCal.py
        ```  
        * To find the Run name: `crtl + W`, search for `file_name` 
            * Change the name of the file for this specific test/chip/date
        * To save: `crtl + o` , `enter`
        * To exit: `crtl + x`

        ```java
        unset PYTHONHOME
        python2 SOAP_HVScan_HiStatCal.py -300 -900 
        ```

        * **For unirradiated HMs**
        ```java
        python2 SOAP_HVScan_HiStatCal.py -200 -900
        ```

        * Hit `enter` when ready to run the test

## Analyzing Test Results

* Before starting the next annealing step, you have to analyze your test results to make sure that you do not need to rerun any of your tests
* Move the run files from the computer (AlibavaGUI folder) into your brux using the WinSCP app
    * Make a folder for each HM diode, and within that folder make a folder for each annealing step `Ann#`
* In Brux, run the analysis to produce the summary files and root files for each test:
    ```java
    cd Alibava (can use cd .. to go back a directory)
    cd Condor     
    ls
    source setup_Alibava.sh
    nano C0_Ann#.txt 
    ```
    * Rename the run file and renavigate to the correct folder. Then save. 
    
    ```java 
    nano Run#####_###_PSS or 2-S.txt
    ```
    * You only need to edit this run file for the first Annealing step
    * `cp “past run file”` `“new run file”` This creates a copy of the past run file and saves it as what your new run file should be called
    * To get the Data to edit this file to fit your current file, you use the Alibava GUI:
        * Produce a text file from the pedestal graph in the Alibava GUI by right clicking on the graph, save as a text file, save it in Documents/AlibavaGUI folder on the computer. Navigate to that text file.
        * This text file contains voltage noise data from each of the 256 pads on the bonding pad of the Alibava Board. To find the locations of the chips, look for spikes in the data. Spikes 60 strips apart signify the first and last strips of the chip. Write these numbers down, rounding up (if 55.5, record 56)
    * When Editing the Run File:
        * `Line 1 = 0 for C0 or 1 for C1`
        * `Line 6 & Line 7 = first strip + 5 &  last strip -5 for C0`
        * `Line 6 & Line 7 = first strip + 5 -127 last strip -5 -127 for C1`
        * `Line 8 = 6   7 originally, before subtracting/adding 5`
        * `Line 9 = time cut = 28  53 = leave the same` 

    ```java
    cd condor    
    ls
    python condor_new.py /isilon/data/users/ctiley/Alibava/Condor/Run#####_###_2-S.txt /isilon/data/users/ctiley/Alibava/Condor/C#_Ann#.txt
    ```
    * Type `condor_q` to see how the data progresses, it should take a few min
        * If something is wrong, AKA running super fast/error, it is most likely a spelling error

    ```java
    cd .. (Condor)
    python LongTermData.py Run#####_###_2-S.txt C#_Ann#.txt 1 7
    ```

    * If this runs correctly, it will bring up a window of some of the root maps for the data. If not, nothing will pop up
    * This will produce summary `files/root` files in your brux account
* In WinSCP, transfer the summary files for the 600V and 800V data into the HEP shared drive: Hep, Testing, Alibava, Summary files folder
* In the excel files for analyzing the summary data (600V and 800V)
    * Click file, go to open, navigate to summary files, open them
    * Copy the data from the summary file into the excel files
* To get the leakage current data, in Brux:

    ```java
    cd Alibava
    cd Soap
    cd Current File
    ls -ltr  (this produces a list of this folders contents, backwards)
    nano “Run file name” 
    ```

    * Copy the data from 600V and 800V, ignoring the negative sign, and past it into the excel doc

* To see the root file graphs, in Brux:

    ```java
    cd Alibava/2S_Irrad_Sensors/Sensor folder /Ann# folder/ 
    source ~/Alibava/Condor/setup_Alibava.sh 
    root (run file name for -600V_0.root)
    ```
    
    * In root server, type in: `TBrowser b`  = opens root browser window
    * go to the root files folder for that HMs data
        * You can search for your desired files/graphs
        * To exit root in brux type `.q`
        * `HitMap.1` = look for excess noise or bad strips (no measurement = 0)
            * We do not want our peaks to be near/within a bad strip
        * `Strip_profile` = should be flat = average charge on each strip
            * Tilt could mean that one part of the chip was closer to the reactor than the other
        * `Noise` = should be around 4-5
            * noise on outer strips is usually higher
            * The noise outside of the bonded area should not affect the data

* Annealing Steps:
* Switch the peltier cables to heating: white = -, red = +
* Plug in the heater cables, black = + red = -
* Turn the yellow lever near the chiller upwards to stop the flow of cold air from the chiller into the alibava set up
* Turn off the wall air
* Set the Annealing temperature in labview, along with the annealing time, hit start annealing button
    * This will cause the PID numbers to go negative in Labview
* 2 minutes before the annealing is set to end, begin to switch the system over to cooling down since the setup will continue to anneal as it cools. It should end up cooling those 2 minutes by the time the system returns to -15°C
    * Switch peltier cables, unplug heating cables, turn on wall air, flip down chiller lever to let air in, unpress the heaters on button in labview, set labview temp to -15°C if running another test


## Annealing Steps

<div class="row">
    <div class="column">
        <div class="card">
            <div class="card__content">
                <div class="card__header">
                    <h4>Step 1</h4>
                </div>
                <ul>
                    <li>Anneal for 20 min the oven at 60°C</li>
                    <ul>
                        <li>Perform strip & interstrip test on HMs in clean room at -20°C</li>
                        <li>Wire bond half moons to the fanout board</li>
                        <li>Annealing test #1: perform alibava test at -15°C</li>
                    </ul>
                </ul>
            </div>
        </div>
    </div>
    <div class="column">
        <div class="card">
            <div class="card_content">
                <div class="card_header">
                    <h4>Step 2</h4>
                </div>
                <ul>
                    <li>Anneal for 60 min in alibava at 60°C = 80 min of annealing total</li>
                    <ul>
                        <li>Annealing test #2: perform alibava test at -15°C</li>
                        <li>Perform diode CV/IV on probe setup at -20°C </li>
                    </ul>
                </ul>
            </div>
        </div>
    </div>
    <div class="column">
        <div class="card">
            <div class="card_content">
                <div class="card_header">
                    <h4>Step3</h4>
                </div>
                <ul>
                    <li>Anneal for 2 hours in the alibava at 60°C (200 min total)</li>
                    <ul>
                        <li>Annealing test #3: Perform alibava test  at -15°C</li>
                    </ul>
                </ul>
            </div>
        </div>
    </div>
</div>

<div class="row">
    <div class="column">
        <div class="card">
            <div class="card__content">
                <div class="card__header">
                    <h4>Step 4</h4>
                </div>
                <ul>
                    <li>Annealing for 30 min at 80°C (500 min total)</li>
                    <ul>
                        <li>Annealing test #4: Perform alibava test at -15°C</li>
                    </ul>
                </ul>
            </div>
        </div>
    </div>
    <div class="column">
        <div class="card">
            <div class="card__content">
                <div class="card__header">
                    <h4>Step 5</h4>
                </div>
                <ul>
                    <li>Annealing for 60 min at 80°C (1100 min total)</li>
                    <ul>
                        <li>Annealing test #5: Perform alibava test at -15°C</li>
                        <li>Remove wirebonds from HMs using tweezers </li>
                        <li>Perform final strip/interstrip test on HMs in clean room at -20°C</li>
                    </ul>
                </ul>
            </div>
        </div>
    </div>
</div>

The initial annealing steps helps improve the performance of the HM strip sensor, but  once it peaks at the 3rd annealing step, the following annealing steps degrad the sensor


## HM Diode CVIV Step after 80min annealing:

* Irradiated Halfmoons: `IT_Postirr_Diodes.cfg` (more steps for increased accuracy)
* Unplug the Hi yellow wire (sends high voltage to the chuck)
    * Unplug the Hi voltage dark yellow wire and Replace it with the light yellow wire that is connected to a box that has a black wire that connects directly to the Alibava board via the green C0/C1 wires
        * This will send the high voltage directly to the Alibava board
        * You have to warm up the setup to 15°C to move the wire from C0 to C1 when testing the diodes
    * Originally ran at -20°C in labview with the chiller set to -10°C, and the wall air pressure set to roughly 25psi
        * NOW, we set it to 0°C in Labview, and set the chiller to 10.3°C
    * NOTE: The depletion region should be around ~200V to 250V
        * make sure the graphs smooth in those areas (no needle movement)
    * Thin black wire = measures CV (needle on the bias ring)
    * Thick Back Wire = measures IV (needle on the bias ring)
        * usually plugged into blue block, will now be directly plugging into needles
    * Green wire = ground - use when measuring CV/IV with the ground ring
    * Originally ran at -20°C in labview with the chiller set to -10°C, and the wall air pressure set to roughly 25psi, dew point roughly -25 to -30°C
        * NOW, we set it to 0°C in Labview, and set the chiller to 10.3°C, dewpoint roughly -8°C to -16°C