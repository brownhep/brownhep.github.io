---
title: CV/IV Station (550 Lab)
tags: HM Test CVIV Irradiation Analysis Probe Station
cover: /assets/images/cover/CVIV_station.jpg
---

# CV/IV Station

The CV/IV station is built for measuring currents in silicon-based diode sensors and pin diodes, as well as for applying and controlling voltage to the chuck or diode, with integrated environmental control.

**CV/IV** stands for:
* **CV**: Capacitance vs Voltage
* **IV**: Current vs Voltage

**Safe Handling Rules**:
Always use gloves when handling irradiated diodes.
**Check** the sensor's temperature before opening its bag.
Never touch the diode with bare hands.
{:.error}


**There are 3 types of diodes:**

**P-type** : HGcal diodes, Half Moon diodes; a negative voltage is applied
{:.info}

**N-type** : D0 diodes (on baggies says CO); a positive voltage is applied
{:.info}

**Pin** : Pin diodes
{:.info}

The damage can be measured by testing IV/CV; this is called particle fluence.

**Particle Fluence** : The amount/degree of radiation that structures have experienced: the damage done. This is measured by the number of radiant-energy particles emitted from or incident on a surface in a given period of time, divided by the area of the surface.
{:.error}

## Setup

* A voltage is set using a ground box and is then transferred to the probe.
    * This probe sets a voltage and then measures the current that results from that voltage.
        * The voltage is set on the big aluminum puck where the diodes are placed. Anything placed on this puck gets set to that same voltage.
        * Two needles are placed onto the diode:
            * One touching the active area of the diode
                * The active area is the working part of the sensor. We can measure how much current flows through it and what the capacitance of the system is when the voltage is increased.
            * One touching the guard ring of the diode
                * The guard ring keeps the voltage going only through the active area, stopping it from traveling through other inactive parts of the diode.

**Capacitance**: A measure of how much charge can accumulate in a certain geometric structure.
{:.info} 

* Increasing the capacitance increases the amount of energy stored.
* A capacitor acts as a way to store energy in a circuit, like a battery.
    * **IV** = Current-voltage measurement (in Amps)
    * **CV** = Capacitance-voltage (in Farads)

## Turning on all components

Turn on the wall air and the power strip for the setup.
* Make sure wall air is at `~60`{:.success}
{:.warning}

Turn on all the temp control and current-measuring machines, ensuring the Julabo is set to the appropriate temperature for the test. 
* Unirradiated diodes are tested at room temperature, 20°C.
    * Set the Julabo to `19.25`{:.success}
    * Set the LabVIEW temperature to 20°C.
* Irradiated diodes are tested at 0°C (HGcal, D0).
    * For 0°C, set the Julabo to -0.5°C.
* Irradiated Half Moons are tested at 20°C.

## LabVIEW

Open LabVIEW. Hit the **run** arrow button, select the load configuration, select the sensor type (P, N, or pin), set the temperature, and hit the **start temp control** button.

IMPORTANT: You need to flip the switch on the setup to either heat or cool for LabVIEW to start controlling the temperature.
{:.warning}

IMPORTANT: The load configuration and sensor type are different for each diode.
{:.warning}

* **Dzeros**: Either `D0_preirr_IV.cfg`{:.warning} or `D0_preirr_CV.cfg`{:.warning} & `N type`{:.info}
    * For irradiated diodes: `D0_postirr_IV.cfg`{:.warning} or `D0_postirr_CV.cfg`{:.warning}
* **Half Moons**: `IT_Diodes_Preirr_IV.cfg`{:.warning}, `IT_Diodes_Preirr_CV.cfg`{:.warning} & `P type`{:.info} or `IT_Postirr_Diodes_Half.cfg`{:.warning} & `P type`{:.info}
    * Unirradiated diodes only need CV tests up to 600V, while irradiated diodes need their CVs tested up to 1000V.
* **HGcal**: `IT_Postirr_Diodes_Half.cfg`{:.warning} & `P type`{:.info}
    * Irradiated: `IT_Postirr_Diodes.cfg`{:.warning}
* **Pin**: `PinDiode_Irrad_HighFluence.cfg`{:.warning} & `Pin`{:.info} type for unirradiated and irradiated

## Filling out the sensor information

Fill out the test information for the specific diode you are testing.

* **File Name**:
    * **HGcal**: `IV`{:.info} or `CV_N####_UR`{:.warning} or `LL_DIODE_GR_Irradiated_Annealed_60C_#min`{:.warning}
        * HGcal diodes are irradiated from 0 to 100 minutes, in ten-minute increments.
        * We test the DIODE and DIODE QUARTER for HgCals with 2 diodes, and DIODE, DIODEHALF, and DIODEQUARTER for HgCals with 3 diodes. Hgcal diodes can either be UL, LL, UR, or LR.
        * Unlike Half Moons, we need to place a needle on the guard ring for HGcal diode measurements.
    * **D0**
        * Pre-irradiation: `IV`{:.info} or `CV_D0_CO###_LargeDiode_GR`{:.warning}
            * We only test the large diode of the D0 diode; the small diode does not have a ground ring.
            * Tests are done before irradiation, directly after irradiation (0 min annealing), and after 80 min of annealing.
    * **Half Moon** 
        * Pre-irradiation: `IV`{:.info} or `CV_#####_###_PSS`{:.warning} or `2-S_HM_XX_DIODE`{:.warning}
        * `DIODE, DIODEHALF`{:.info}, `DIODEHALFPSTOP`{:.info}, `DIODEHALFPSTOP_GR`{:.info}, `DIODEQUARTER`{:.info}
        * For HMs, we only use the bias needle when running the test. The ground needle is only used when testing DIODEHALFPSTOP.
    * **Pin** 
        * Pre-irradiation: `Pin###`{:.warning}
* For the annealing status, either write "Not irradiated." If the diode has been irradiated, write:
    * **Irradiated and annealed at ___°C for ___ minutes**

<div class="card">
  <div class="card__content">
    <div class="card__header">
      <h4>DIODE Annealing steps:</h4>
    </div>
    <ul>
      <li>Set oven to warm up to 60°C.</li>
      <li>Use the oven under the benchtop along the wall with a dehumidifier.</li>
      <li>Use heat gloves to take the aluminum plate from the oven.</li>
      <li>Place the diodes on the aluminum plate so the tip sticks off (for easy removal).</li>
      <li>Place the diode in the oven to anneal for ___ minutes (set a timer).</li>
      <li>When remeasuring the diode, change the annealing status and file name to account for additional annealing time.</li>
      <li>Take the diode from the oven and place it in the freezer until ready to measure.</li>
      <li>Run CV/IV for the diode.</li>
    </ul>
  </div>
</div>

## Selecting the CV/IV test

Make sure you flip the switch to CV or IV depending on which test you are running.

## Placing the diodes

* **Unirradiated diodes** are stored in dry boxes at room temperature, so you can open their baggies right away and place them in the test box.
* **Irradiated diodes** are stored in the freezer and need to sit on the testing bench until they reach room temperature before their bags can be opened.
    * We do not want humidity changes to cause water droplets to form on the diodes.
* Do not touch diodes with bare hands, and do not put fingers inside their baggies. Use plastic-tipped tweezers to remove the diode from the bag, and use the vacuum pen to place it in the plastic test box.
* Place the diode onto the vacuum holes on the platform (if testing more than one diode, do not let the diodes touch).
    * **Dzero**: Place horizontally with the large diode on the right.
    * **Half Moon**: Place vertically with the diode side facing the wall.
    * **Pin Diodes** are not placed into the test box:
        * Move the yellow High_In wire (plugged in next to the CV/IV switch) and plug it into the hexagon-shaped box on top of the current measuring units (at the spot labeled Hi In).
        * Connect the black hook wire to the larger terminal on the pin diode and the red hook wire to the small terminal.
            * Make sure the red side of the diode is facing up.
        * In LabVIEW, skip the temperature control and start the CV/IV test.
* When placing the diode, use the vacuum and the magnifier to place the needles. Make sure the guard needle is on the guard ring.
    * **Half Moons**: Use only the bias needle on `DIODE`{:.info} and `DIODEQUARTER`{:.info}. When using `DIODEHALF`{:.info} or `DIODEHALFPSTOP`{:.info}, place the second needle (guard) on the guard ring.
* Unirradiated diodes do not need extra room temperature equilibration time between each test. Irradiated diodes require additional temperature stabilization time between tests.