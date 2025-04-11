---
title: MaPSA Test
tags: Test MaPSA MPA Probe Tesla
cover: /assets/images/cover/MaPSApic.png
---

# MaPSA Probe Testing

The Macro Pixel Sub-Assembly (MaPSA) is the bump bonded assembly of the
pixelated PS-p sensor and the MPA (Macro Pixel ASIC) readout chip. The PS modules contain a strip sensor on the top layer and a the pixelated strip sensor on the bottom layer. This will require sixteen MPA chips (each with a size of 12 mm x 26mm and containing 1918 bumps) to be connected to a single large area sensor piece.


## Details about the MaPSA

* 2x8 MPA chips
* 1 PS-p sensor per assembly
* Pixels are on a 1446x200 μm pitch
    * 200 μm pitch is staggered (effective 283 μm pitch)
* From the first wirebond pad of 1 MPA to the next MPA first wirebond pad is 12mm. `Important`{:.error}
* MPA chips have 118 wirebond pads on 100 micron pitch. 
* Each pad has a 100x70 micron region for probe testing.


## Setting things up

* Turn on the wall air
    * Located in the back of the prober, the second handle.

<div class="card">
  <div class="card__image">
    <img class="image" src="/assets/images/MaPSA/s-l1600.jpg"/>
  </div>
  <div class="card__content">
    <div class="card__header">
      <h4>Power Supply</h4>
    </div>
    <p>Turn only the Output</p>
  </div>
</div>

* Press the green button of the Tesla Prober
    * This is to initialize the Prober
* Inside the Prober, check if the Probe Card is on
    * It has a red LED indicator
* Turn on the FC7 by turning the switch towards the user 


## Setting up the GUI

* Connect to the FC7
  * Ethernet Connection named `enp2s0`{:.info}
* `If the terminal is not on root:`{:.warning}
    * ```java
    cd Documents/MaPSA/MaPSA_Testing/Ph2_ACF
    su //This requires a password, ask supervisor
    source setup.sh
    ```
* Initialize the FC7 and Probe Card
  * ```java
    fpgaconfig -c settings/MaPSAstation.xml -i uDTC_MPA_SEU_Dev_PM.bin
    fpgaconfig -c settings/MaPSAstation.xml -l
    ```
* Run the GUI
  * ```java
    cd MPA2_Testing/MPA2_Test/
    ./start_minigui_mpa.sh
    ```

* On the terminal its going to output:

```java
IP=192.168.0.8
______________________________________________________
             Starting MPA2 Test System                 
                                                      

PING 192.168.0.8 (192.168.0.8) 56(84) bytes of data.
64 bytes from 192.168.0.8: icmp_seq=1 ttl=64 time=0.058 ms

--- 192.168.0.8 ping statistics ---
1 packets transmitted, 1 received, 0% packet loss, time 0ms
rtt min/avg/max/mdev = 0.058/0.058/0.058/0.000 ms
=>  MPA Testbench correctly found at address 192.168.0.8
=>  Loading scripts
->  Board Selected MAC > 08:00:30:00:29:61 IP > 192.168.0.8
->  Loaded configuration for MPA
```

* When the GUI launches it should look like this:
![MaPSA GUI](/assets/images/MaPSA/GUI1.png)


## MaPSA

### Step 1: Take the MaPSA

* Take the MaPSA out of the dry box
* Open the compartment of the prober

The most reliable way to check the first MPA is by turning the MaPSA around and check the PS for this corner:

<div class="grid">
  <div class="cell cell--auto">
    <img src="/assets/images/MaPSA/MPA1.jpg" alt="First MPA">
  </div>
  <div class="cell cell--shrink">
    <p><b>Or:</b></p>
  </div>
  <div class="cell cell--auto">
    <img src="/assets/images/MaPSA/MaPSA_box.jpg" alt="MaPSA box">
  </div>
  <div class="cell cell--4">
    <ul>
      <li>Turn around the MaPSA box and locate a flat corner in the box</li>
      <ul>
        <li><b>IF</b> its Hamamatsu (this will be explained in Step:6)</li>
      </ul>
      <li>This flat corner locates the <b>First MPA</b> of the MaPSA</li>
    </ul>
  </div>
</div>

### Step 2: Placing the MaPSA

<div class="grid">
  <div class="cell cell--auto">
    <img src="/assets/images/MaPSA/MaPSA_pins.jpg" alt="MaPSA Pins">
  </div>
  <div class="cell cell--4">
    <ul>
      <li>Using the vacuum pen take the MaPSA and place it between the white pins on the chuck</li>
      <li>Close the compartment of the prober</li>
    </ul>
  </div>
</div>


### Step 3: Setting up the Z-axis 

<div class="grid">
  <div class="cell cell--auto">
    <img src="/assets/images/MaPSA/Velox.jpg" alt="Velox">
  </div>
  <div class="cell cell--4">
    <ul>
      <li>On the prober's computer select <b>Home icon</b> <img src="/assets/images/MaPSA/Home_icon.jpg" width="25" height="25" alt="Home icon"> </li>
      <li>Lift the chuck by using the arrows in the Z setup</li><img src="/assets/images/MaPSA/arrows.jpg" width="10%" height="10%" alt="Arrows">
      <ul>
        <li>Lift the chuck up until you see faintly the MaPSA and make sure that the needles are in the pads</li>
      </ul>
    </ul>
    <center><img src="/assets/images/MaPSA/Z-setup.jpg" width="50%" height="50%" alt="Z-setup"></center>
  </div>
</div>


### Step 4: Alignment

![MaPSA Pads](/assets/images/MaPSA/MaPSA_pads.png)

<div class="grid">
  <div class="cell cell--auto">
    <img src="/assets/images/MaPSA/pads.png" alt="Pads">
  </div>
  <div class="cell cell--4">
    <ul>
      <li>MaPSA pads are divided in two sections: </li>
      <ul>
        <li>Wirebond area ~100μm x 70μm</li>
        <li>Probing area (closer to the sensor) ~200μm x 70μm</li>
      </ul>
    </ul>
  </div>
</div>

* To align the prober:

<div class="grid">
  <div class="cell cell--auto">
    <img src="/assets/images/MaPSA/Velox.jpg" alt="Velox">
  </div>
  <div class="cell cell--4">
    <ul>
      <li>Select the Manual Alignment button</li>
      <li>Select two corners in the pads to align the MaPSA</li>
    </ul>
  </div>
</div>

* Now that the prober is aligned with the pads of the MaPSA, position the crosshair on top of the previous probing marks on the pads.
  * Sometimes is required to adjust the needles
  * You can see where the needles are making contact by adjusting the focus of the microscope
  * You can move side to side using the back dial from the microscope

### Step 5: Make contact

* Lower the needles using <img src="/assets/images/MaPSA/lower_needles.jpg" width="10%" height="10%" alt="Arrows"> on the Z Setup
  * `Red box`{:.error} :No contact
  * `Yellow box`{:.warning} :Before contact
  * `Green box`{:.success} : **Contact** 

### Step 6: Fill in the info

* There is two different vendors that supplies the MaPSAs
  * Hamamatsu
  * QPT

To identify the vendors:
<div class="grid">
  <div class="cell cell--auto">
    <img src="/assets/images/MaPSA/Vendors.jpg" alt="MaPSA box vendors">
  </div>
  <div class="cell cell--4">
    <ul>
      <li>Envelope: <b>QPT</b></li>
      <li>Case cover: Hamamatsu <b>HPK</b></li>
    </ul>
  </div>
</div>

* On MaPSA ID:

```java
HPK_XXXXX_XXX[X] (If its Hamamatsu)
QPT_XXXXX_XXX[X] (If its QPT)
```

* The final character being the letter of the side of the MaPSA (**L**eft or **R**ight)

![MaPSA GUI](/assets/images/MaPSA/GUI1.png)

* On the MPA box fill in the number of the current MPA being tested.
  * `Note`{:.warning} that each time the user finish testing one MPA and moves the needles to the next MPA, the user has to change this number manually, otherwise it **WILL** overwrite the data


### Step 7: Run the initial tests

* Click on `Power On` button
* On the terminal you should see something like this
```java
->  SSA enabled 
->  MPA enabled 
---> Enabling the MPA SSA Board I2C master
---> Enabling the MPA SSA Board I2C master
->     Sent Hard-Reset pulse 
->  P_dig:  74.130mW  [V=  0.983V - I= 75.450mA]
->  P_ana:  71.609mW  [V=  1.222V - I= 58.600mA]
->  P_pad:   9.840mW  [V=  1.230V - I=  8.000mA]
->  Total: 155.579mW  [             I=142.050mA]
... more stuff ...
Line Status: 
   Tuning done/applied: 1
   Line ID: 5,   Idelay: 5,   Bitslip: 6,   WA FSM State: 14,   PA FSM State: 14
Line Status: 
   Tuning done/applied: 1
   Line ID: 5,   Idelay: 5,   Bitslip: 6,   WA FSM State: 14,   PA FSM State: 14
->     Initialised SLVS pads and sampling edges
->     Sampling phases tuned
->     Activated normal readout mode
```

* If the contact is not good, you will get an output with the Total Power and current numbers off by 10-20 mW or even 100mW!
  * Additionally it can output an error
    * Check the Troubleshoot for help
* After this, click `Pixel Alive`
* This will generate a plot with the status of the pixel and if it has noise or other problem with it (Operational)


### Step 8: Run MPA test

* The Pixel Alive should be 100 in the heat map
* After this run the `IV Scan`
  * This takes ~8 minutes

![MaPSA GUI2](/assets/images/MaPSA/GUI2.png)
* After it finishes, go to `Plotting` tab and click on `Draw IV` 
  * This test runs up to -800V and as voltage goes up, the current goes up (Ohm's Law)
  * An example of the first voltage and current taken and last
  * 
    | Voltage    | Current |
    | -------- | ------- |
    | -10.00  | -0.09    |
    | -800.00 | -0.35     |


### Step 9: Run MPA test

* Go back to the `Manual MPA test` tab and click `Test 1 MPA`
  * Check if the `Power On` is active
* This will test:
  * Wafer test
  * Mask/Alive
  * Pretrim S
  * Prosttrim S
  * Bad Bump
* This test should take ~4.5 minutes (for each MPA)
* After it finishes, click `Plotting` tab

![MaPSA GUI2](/assets/images/MaPSA/GUI2.png)

* Click `Draw 2D summary plots`
* This will plot the current and previous MPA tested
* Check if the data is sensible, if so, then repeat `Step 4` - `Step 5` and `Step 9` 


## Troubleshoot 🛠️

### :warning: **Error:** After Pixel Alive

```java
pyvisa.error.VisaIOError: VI_ERROR_RSRC_BUSY (-1073807246): The resource is valid, but VISA cannot currently access it.
```
:memo: **Solution:** USB connection error
* Disconnect the white long USB Type A (on the floor)
* Reconnect USB
* Try again **Pixel Alive**

### :warning: **Error:** No plot after Pixel Alive and the following error: 

```java
Line Status:
  Tuning done/applied: 0
  Line ID: 4,   Idelay: 15,   Bitslip: 7,   WA FSM State: 13,   PA FSM State: 14
Line Status:
  Tuning done/applied: 0
  Line ID: 4,   Idelay: 15,   Bitslip: 7,   WA FSM State: 13,   PA FSM State: 14
Failed tuning line 4
Line Configuration:
  Line ID: 5,   Mode: 0,    Master line ID: 0,    Idelay: 0,    Bitslip: 0
Line Status:
  Tuning done/applied: 0
  Line ID: 5,   Idelay: 0   Bitslip: 0    WA FSM State: 0   PA FSM State: 12

Line Status:
  Tuning done/applied: 0
  Line ID: 5    Idelay: 0   Bitslip: 0,   WA FSM State: 0,    PA FSM State: 12
Line Status:
  Tuning done/applied: 0
  Line ID: 5,   Idelay: 0,  Bitslip: 0,   WA FSM State: 0,    PA FSM State: 12
Failed tuning line 5
-> Initialised SLVS pads and sampling edges
-> Sampling phases tuned
-> Activated normal readout mode
('ASRL1: : INSTR', 'ASRL2 : : INSTR', 'ASRL3: : INSTR', "ASRL4: : INSTR')

KEITHLEY INSTRUMENTS INC.,MODEL 2410,4457440, C34 Sep 21 2016 15:30:00/A02 /K/M
Fail: 2
Fail: 2
Exception in Tkinter callback
Traceback (most recent call last):
  File "/usr/lib64/python3.6/tkinter/_init_.py", line 1705, in__call__
    return self.func(*args)
  File "/home/jluo/Documents/MaPSA/MaPSA_Testing/MPA2_Testing/MPA2_Test/main.py", line 425, in pa
    pixel_alive = mpa.cal.pixel_alive(ref_cal=cal, ref_thr=thr, pulse_delay=delay, plot=1)
  File "/home/jluo/Documents/MaPSA/MaPSA_Testing/MPA2_Testing/MPA2_Test/mpa_methods/mpa_cal_utility.py", line 334, in pixel alive
    tempnom = self.conf.convertRawToNomPixmap(temp)
  File "/home/jluo/Documents/MaPSA/MaPSA_Testing/MPA2_Testing/MPA2_Test/myScripts/mpa_configurations.py", line 74, in convertRawToNomPixmap
    nomdata.append(data[p])
TypeError: 'int' object is not subscriptable
```
:memo: **Solution:** Bad connection
* Press **Power Off** on the GUI to power off the MPA
* Reposition the needles (no more than 5µm in X or Y) and try again.

Other examples of bad connection:

<center>
<div class="row">
  <div class="column">
    <img src="/assets/images/MaPSA/noise1.png" alt="Noise 1">
  </div>
  <div class="column">
    <img src="/assets/images/MaPSA/noise2.png" alt="Noise 2">
  </div>
  <div class="column">
    <img src="/assets/images/MaPSA/noise3.png" alt="Noise 3">
  </div>
</div>
</center>

## References 📝

* [MaPSA ASSEMBLY Testing Specification](https://indico.cern.ch/event/916520/contributions/3853044/attachments/2035348/3407469/MPA_Test_proto.pdf)
* [MaPSA Overview](https://indico.fnal.gov/event/21632/contributions/63861/attachments/40206/48740/B04-MaPSA-Berry-CD1-2019.pdf)
* [MaPSA Twiki](https://twiki.cern.ch/twiki/bin/viewauth/Sandbox/MaPSAProbeTesting)