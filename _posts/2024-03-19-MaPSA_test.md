---
title: MaPSA Test
tags: Test MaPSA MPA Probe Tesla
cover: /assets/images/cover/
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
    <img class="image" src="/assets/images/s-l1600.jpg"/>
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
    source setup.sh
    su
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


## Testing MPAs

* When the GUI launches it should look like this:
![MaPSA GUI](/assets/images/GUI1.png)
