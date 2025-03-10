---
title: Tesla Probe Machine in Clean Room
tags: HM Test CVIV Irradiation Analysis Clean Room Probing Strip
cover: /assets/images/cover/Probe_station.jpg
---

**Before starting** The vacuum pen, needs to be cleaned before starting any test.
{:.error}

To clean the vacuum pen:
* Grab a Kim Wipe and Isopropyl Alcohol (Bottle with yellow dispenser cap)
* Wipe the vacuum pen's suction cup 
* Dry the vacuum pen using the ion fan for 10 - 15 seconds.

This will ensure that the vacuum pen doesn't transfer any dust to the sensors and potentially scratch them or damage them due to friction and static. Additionally to undesired marks of the vacuum pen on the sensor.

## Tesla200

The probing machine in the clean room is a Cascade Tesla200, a 200 mm semi-/ fully-automated on-wafer power device characterization system. The Tesla200 on-wafer power semiconductor probing system is engineered to provide accurate data up to 3 kV (triaxial) / 10 kV (coaxial) and 200 A (standard) / 600 A (high current).

<div class="item">
  <div class="item__image">
    <img class="image image--lg" src="https://www.formfactor.com/wp-content/uploads/TESLA200-animated.gif"/>
  </div>
</div>

In the clean room we currently have 2 Tesla200:
1. For MaPSA
2. For probing tests
    * CV/IV
    * Strip testing

The Tesla machine that we are going to concentrate on this manual is located at the right end of the clean room.

# CVIV Machine in Clean Room

When new sensors arrive, they are first visually inspected and then are ran in the CVIV machine to produce their CV/IV curves. The CV/IV tests predict the behavior of the sensors, optimize material and design choices for future applications.

The worse (i.e. breakdowns occur) sensors are then strip tested (additional needles on the machine) and then tested long term with Andre. 

## CVIV Procedure

* Open up the door of the Tesla200
* Lift down the cubby door, pull out the large platform. This large platform is called a **wafer**. Turn on the **ion fan** (blows out +/- ions to neutralize charged items; increases in humidity makes it easier for charges to build up)
* Wearing an ESD bracelet, remove the sensor from its envelope or ziplock bag.
    * Unirradiated sensors are kept in dry boxes around the clean room.
    * Radiated sensors are usually kept in a fridge in 550 room
* Using the vacuum pen, place the sensor, carefully to android the needle, down onto the round platform. The tape is there to ensure that the sensor does not fly off the platform. Cover up all the vacuum holes with the sensor. One you have lined up the sensor to the bottom left corner of the setup, turn on the vacuum by flipping the 2 switches to the left inside the cubby labeled 1 & 2.
    * For **HM**, remove the sensor using plastic-tip tweezers. Place the diode on the platform horizontally, aligning the stripside in the lower left corner.
    * Flip the single dial switch on the right side of the cubby, this only turns on the vacuum for the diodes (small)
* Then, push in the round platform, lock it into place, and close the cubby door.
* Turn on the probe station by hitting the green start button on the right side of the doorway. This activates the software that comes with the probe station. Open labview on the computer on the desk. 
* Click on the home button on the screen, this moves the needle into the home position (moves the whole round platform deeper into the cubby). Then click on the light bulb button to turn on the microscope’s light, then raise the platform by clicking the separate needle from sensor button. 
* The controller that comes with the probe has a dial to adjust the focus, amount of light, and the zoom used by the microscope. 
* NOTE: We want to touch the needle to bias ring of the sensor.
    * Each sensor has strips and at the end of each strip is a pad that is connected to the bias ring by a resistor. The bias ring designates the active area of the sensor that the voltage/current will run through.
* Open the cubby up and without moving the round platform, use the knobs on the needle base to move the needle so that it is making contact with the bias ring 
* The probing process is light sensitive, so before running, close the blinds on the black box.
* In labview, click enter run info, and then scan the barcode on the sensor’s envelope to enter the sensor's name. The click no for “is it irradiated?”, enter the tester’s name (yourself), and any notes.
    * Labview then auto populates all the other information based on the sensor’s barcode.

IMPORTANT: For IV, flip the switch to **IV mode**, and then put the bias (green) wire into the top right Kethley machine (kethley machines are the high voltage supply and measure the IV/CV). This connects it to the bias ring. 
{:.warning}

* Plug the AC wire into the ac pad
    * For CV, flip the switch to **CV mode**, and then move the green wire back to the AC Pad near the IV/CV switch, leave the AC wire unplugged
    * For IV, if the bias voltage is on (light glows on Kethley and the bias voltage button in the program will be bright) and you open the door to the black box, the program will automatically shut the voltage off
    * The voltage gets sent through the round platform and then into the sensor
    * The max voltage for both IV and CV is 1000 volts. However, as a safety, the CV only goes up to 600 volts, incase of any breakdowns observed when running the IV
    * The temperature of the whole setup is set to ~23.5 degrees C (has a chiller to control temp). The higher the temperature, the higher the current
    * The CV graph levels off by 200 volts
    * The depletion voltage is usually around 215 volts
    * If something looks wrong on one of the graphs, hit the stop button to cancel the run. 
    * Normal starting numbers are around E^-5 to -8, and normal final for IV are around 1.5 - 2.0E^-7 
* On the top screen, in the section labeled “Material Handling”, hit the center button to move the round platform back into the load position. Then Hit the first button (unload) to move the platform to the front of the cubby
* Wearing an ESD bracelet, pull out the platform, turn off the vacuum, lift the bias needle push the sensor back lightly with the plastic tweezers so as not to have it hit the needle, and then use the vacuum pen to pick up the sensor and repackage it in its envelope. Then place the sensor back into the drybox. 
* Data is saved in `Local Dish (c:) - strip measurements - data`
    * Named the following: CV or IV_Sensor Name_date_time
* When all of the 2S Sensor data is collected, copy all the text files and put them into the shared HEP drive: `HEP_shared - pre production - CVIV - batch # - specific sensor`
    * As noted above, abnormal sensors receive further testing
    * Diodes get saved to `HEP_shared - pre production - Irradiation studies - data - preirrad or postirrad - 2S or PSs - specific batch number - diode number`
        * In the clean room, we test the strip sensor on the halfmoon diodes. In 550, we test the diodes themselves. All of this data gets saved in this same folder.


# Strip Testing

Strip testing is done to sensors to test out the strips. For the **HM** each strip is tested since its very small (compared to the other sensors) and test runs faster. In the other hand, **2S** and **PSS sensors**, we have to skip some strips (4 strips) in order to make the test faster. 

**2S sensors has 2032 strips, distributed in two rows of 1016 strips.The PSS sensors has 1920 strips distributed in two rows of 960 strips.**

Useful for allignment.
{:.info}

## Procedure for Strip Testing

IMPORTANT: for strip tests we want the probe set to IV mode, not CV, so everything will be set up as if we were running the IV test: flip the switch to IV mode, and then put the bias wire into the top right Kethley machine Plug the AC wire into the ac pad 
{:.warning}

### HM

* Wearing an ESD bracelet, remove the halfmoon from the plastic bag using plastic-tip tweezers. Place the diode on the platform horizontally, aligning the stripside in the lower left corner.
* Flip the single dial switch on the right side of the cubby, this only turns on the vacuum for the diodes (small)
* Push in the platform, close the cubby, turn on the probe station
* Hit the home button, turn on the light, hit the separate needle from sensor button, and focus the microscope
    * NOTE: IF when clicking the home button home is way off the sensor, then on the top screen go to: FILE - MAP - OPEN - 2S_irrad_sensor(Or corresponding sensor) 
        * This should put the needle in the correct map when running our test. When Nick #2 uses the probe, he switches to a different map to run his tests.
* In Labview, click enter run info, type in `39567_045_2-S_HM_XX`
* Before running strip test, run the CV/IV by placing the bias needle on the bias ring 
* Once CV/IV is ran, flip the switch back into strip mode, connect the bias wire to the keithley, and plug in the ac pad wire
* FIRST, align the sensor. Hit the 2 point alignment button and on the strip hit 2 points on the ends of the same strip that make a straight line = this aligns the whole set-up to this orientation
* Set home to strip one in the top right corner of the strip sensor on the halfmoon diode
    * Each strip is composed of a long metal strip connected to a conductor at each end. This conductor is like a sandwich & is composed of a DC pad (bottom) , an insulator, and an AC pad (top). This insulator ensures there is no contact being made between the AC and DC pads. The DC pad sticks out from underneath the AC pad and appears to be the shorter pad to the right of the AC pad. Place the right needle (DC needle) over the DC pad and the left needle (AC needle) over the AC pad. Roughly center each needle on the pads. 
    * Right click the home button and click set to current location 
* To ensure that the needles will be centered on the pads for each strip, we can move the probe station manually: In Labview, go to the “Move probe station” tab, and enter the pad number in “go to pad” that you want to check: CHECK PAD #59. Look to make sure the needles still look centered above the pads
* Since both needles are testing pads on the same strip, this strip test is called the SINGLE test. Therefore, in Labview, click single and then click SCAN to start running the test 
* For both strip tests, the keithley ramps up to 600 volts and stays there for each strip
* The SINGLE test runs 5 tests: 
    * Global current = the IV (current voltage) at 600 volts = stays @ roughly 2 - 3 E-9
    * Pinhole = applied voltage between the AC & DC pads; makes sure there are no holes that connect/short the pads
        * Stays at zero unless there is a pinhole 
    * Coupled Capacitance = measures the capacitance between AC/DC 
        * stays stable slightly above zero
    * DC leakage = how much current leaks out for each individual strip 
        * Stays @  roughly 1 E-10/-11
    * R Bias = measures the resistance of the snake resistor
        * Stays at roughly 1.5 E-6
* If the needles are not making good contact, the readings will show a spike in these graphs
    * The allowed number of bad measurements before a forced run stop is 3. After all 60 strips are ran, you can go back and retest the bad strips
        * In labview run test tab, go to “pads to retest” type in the pad number” and hit retest pads
        * The program will automatically add the reran strip measurements at the bottom of the text file generated for this test. 
        * You can check which pad failed to make contact by checking the text file for the test.
* Once the SINGLE test is complete, you can then run the INTERSTRIP test
    * To run the Interstrip test, the AC needle needs to move to the DC Neighbor pad: this is the DC pad directly below the first/previous pad
    * Then, switch the AC wire connected to the AC needle with the DC Neighbor wire 
    * Make sure you check that the needles are centered by going to the 59th/60th pad 
    * Then, in labview, hit the interstrip button and then hit scan to begin the test
* The INTERSTRIP test runs 3 tests 
    * Global current = the IV at 600 volts = stays @ roughly 2 - 3 E-9
    * Interstrip capacitance = forms an elongated arch shape because the strips closest to the sides of the sensor have a lower capacitance due to a lack of neighboring strips 
        * Stabilizes at ~5.4E-12
    * Interstrip resistance = stays between E-9 to E-11
    * Spikes (downward for capacitance, upward for resistance) form when the needle fails to make contact with the pads. If a spike occurs, just like for the Single Test, you can retest that specific pad. 
    * The other tests (pinhole, coupling capacitance, DC leakage, RBias, etc) should remain at zero/blank since they deal with the relationship between the AC and DC pads.
* When all of the data is collected, copy all the text files and put them into the shared HEP drive: 

```yaml
HEP_shared - Pre Production - StripMeasurements - specific sensor number folder
``` 


### 2S and PSS sensors

The procedure is similar to the HM but due to the size, it requires a special handling to avoid error/or propagate them.

* Change the shoes covers to an ESD shoe cover (blue ones with black strap)
    * Black strap in shoe cover must be facing to the floor, and tucked inside with socks and touching the skin.
* Lift down the cubby door, pull out the large platform. This large platform is called a **wafer**. Turn on the **ion fan** (blows out +/- ions to neutralize charged items; increases in humidity makes it easier for charges to build up)
* Wearing an ESD bracelet, remove the sensor from its envelope.
    * Unirradiated sensors are kept in dry boxes around the clean room.
    * Radiated sensors are usually kept in a fridge in 550 room
* Using the vacuum pen, place the sensor, carefully to android the needle, down onto the round platform. The tape is there to ensure that the sensor does not fly off the platform. Cover up all the vacuum holes with the sensor. One you have lined up the sensor to the bottom left corner of the setup, turn on the vacuum by flipping the switches to the left inside the cubby labeled.
    * For 2S, flip **1 & 2 switches**
    * For PSS, flip **switch 1**
* Place the ion fan on top of the sensor and turn it on for **10 minutes**
* Then, push in the round platform, lock it into place, and close the cubby door.
* Turn on the probe station by hitting the green start button on the right side of the doorway. This activates the software that comes with the probe station. Open labview on the computer on the desk. 
* Click on the home button on the screen, this moves the needle into the home position (moves the whole round platform deeper into the cubby). Then click on the light bulb button to turn on the microscope’s light, then raise the platform by clicking the separate needle from sensor button. 
* The controller that comes with the probe has a dial to adjust the focus, amount of light, and the zoom used by the microscope. 
* NOTE: We want to touch the needle to bias ring of the sensor.
    * Each sensor has strips and at the end of each strip is a pad that is connected to the bias ring by a resistor. The bias ring designates the active area of the sensor that the voltage/current will run through.
* Open the cubby up and without moving the round platform, use the knobs on the needle base to move the needle so that it is making contact with the bias ring 
* The probing process is light sensitive, so before running, close the blinds on the black box.
* In labview, click enter run info, and then scan the barcode on the sensor’s envelope to enter the sensor's name. The click no for “is it irradiated?”, enter the tester’s name (yourself), and any notes.
    * Labview then auto populates all the other information based on the sensor’s barcode.
* Once **CV/IV** is ran, flip the switch back into strip mode, connect the bias wire to the keithley, and plug in the ac pad wire
* Align the sensor. Hit the 2 point alignment button and on the strip hit 2 points on the ends of the same strip that make a straight line = this aligns the whole set-up to this orientation
* Set home to strip one in the top right corner of the strip sensor
    * Each strip is composed of a long metal strip connected to a conductor at each end. This conductor is like a sandwich & is composed of a DC pad (bottom) , an insulator, and an AC pad (top). This insulator ensures there is no contact being made between the AC and DC pads. The DC pad sticks out from underneath the AC pad and appears to be the shorter pad to the right of the AC pad. Place the right needle (DC needle) over the DC pad and the left needle (AC needle) over the AC pad. Roughly center each needle on the pads. 
    * Right click the home button and click set to current location 
* To ensure that the needles will be centered on the pads for each strip, we can move the probe station manually: In Labview, go to the “Move probe station” tab, and enter the pad number in “go to pad” that you want to check: **CHECK PAD #**. Look to make sure the needles still look centered above the pads
    * For 2S **CHECK PAD #1016**
    * For PSS **CHECK PAD #960**
* Since both needles are testing pads on the same strip, this strip test is called the SINGLE test. Therefore, in Labview, click single and then click SCAN to start running the test 
* For both strip tests, the keithley ramps up to 600 volts and stays there for each strip
* The SINGLE test runs 5 tests: 
    * Global current = the IV (current voltage) at 600 volts = stays @ roughly 2 - 3 E-9
    * Pinhole = applied voltage between the AC & DC pads; makes sure there are no holes that connect/short the pads
        * Stays at zero unless there is a pinhole 
    * Coupled Capacitance = measures the capacitance between AC/DC 
        * stays stable slightly above zero
    * DC leakage = how much current leaks out for each individual strip 
        * Stays @  roughly 1 E-10/-11
    * R Bias = measures the resistance of the snake resistor
        * Stays at roughly 1.5 E-6
* If the needles are not making good contact, the readings will show a spike in these graphs
    * The allowed number of bad measurements before a forced run stop is 3. After all 60 strips are ran, you can go back and retest the bad strips
        * In labview run test tab, go to “pads to retest” type in the pad number” and hit retest pads
        * The program will automatically add the reran strip measurements at the bottom of the text file generated for this test. 
        * You can check which pad failed to make contact by checking the text file for the test.
* Once the SINGLE test is complete, you can then run the INTERSTRIP test
    * To run the Interstrip test, the AC needle needs to move to the DC Neighbor pad: this is the DC pad directly below the first/previous pad
    * Then, switch the AC wire connected to the AC needle with the DC Neighbor wire 
    * Make sure you check that the needles are centered by going to the 59th/60th pad 
    * Then, in labview, hit the interstrip button and then hit scan to begin the test
* The INTERSTRIP test runs 3 tests 
    * Global current = the IV at 600 volts = stays @ roughly 2 - 3 E-9
    * Interstrip capacitance = forms an elongated arch shape because the strips closest to the sides of the sensor have a lower capacitance due to a lack of neighboring strips 
        * Stabilizes at ~5.4E-12
    * Interstrip resistance = stays between E-9 to E-11
    * Spikes (downward for capacitance, upward for resistance) form when the needle fails to make contact with the pads. If a spike occurs, just like for the Single Test, you can retest that specific pad. 
    * The other tests (pinhole, coupling capacitance, DC leakage, RBias, etc) should remain at zero/blank since they deal with the relationship between the AC and DC pads.
* When all of the data is collected, copy all the text files and put them into the shared HEP drive: 

```yaml
HEP_shared - Pre Production - StripMeasurements - specific sensor number folder
``` 

