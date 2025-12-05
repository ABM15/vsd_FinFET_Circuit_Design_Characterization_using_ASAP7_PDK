# FinFET Circuit Design and Characterization
This GitHub repository documents the 10-day workshop on [FinFET Circuit Design and Characterization using ASAP7 PDK](https://www.vlsisystemdesign.com/7nm) offered by VSD Corp. Pvt. Ltd. attended as part of cohort 28 Nov - 7 Dec, 2025.
<br/>

**Table of Contents**

 | Module # | Topic(s) Covered |
 |---|---|
 |[**Mod. 1**](#1---scaling-beyond-cmos-finfet-devices-and-innovations) | **Scaling Beyond CMOS: FinFET Devices and Innovations** <br> <ol> <li>[Path To Zetta Scale Computing](#11---path-to-zetta-scale-computing)</li> <li>[Introduction To FinFETs](#12---introduction-to-finfets)</li> <li>[FEOL Innovations](#13-feol-innovations)</li> <li>[BEOL Innovations](#14---beol-innovations)</li> </ol> |
 |[**Mod. 2**](#2---lab-to-simulation-7nm-finfet-inverter-performance-analysis) | **Lab-to-Simulation: 7nm FinFET Inverter Performance Analysis** <br> <ol> <li>[NFET DC Characteristics Using 7nm PDKs](#21---nfet-dc-characteristics-using-7nm-pdks)</li> <li>[First Inverter Characteristics Using 7nm FinFETs](#22---first-inverter-characteristics-using-7nm-finfets)</li><li>[Module 2 Assignment - 7nm Inverter Characterization](#23---module-2-assignment---7nm-inverter-characterization)</li> </ol> |
 |[**Mod. 3**](#3---design-of-a-bandgap-reference-circuit) | **Design of a BandGap Reference Circuit** <br> <ol> <li>[Theory: Design of a BGR Circuit](#31---theory-design-of-a-bgr-circuit)</li> <li>[Module 3 Assignent - Bandgap Reference Design and Simulation using Xschem](#32---module-3-assignent---bandgap-reference-design-and-simulation-using-xschem)</li> </ol> |


## 1 - Scaling Beyond CMOS: FinFET Devices and Innovations
### 1.1 - Path To Zetta Scale Computing

| ![Mod1_lecture_01c](/docs/images/lecture_screenshots/Mod1_lecture_01c.png) |
|:---:|

#### 1.1.1 - CMOS Evolution And Next-Gen Candidates

As CMOS technology approaches sub-1 nm nodes, conventional Dennard scaling has essentially ended, and further device scaling must rely on innovations across multiple domains: Patterning, Channel Engineering, Gate Stack Innovation, Interconnect Scaling, Device Architecture, and Design-Technology & System-Technology Co-Optimization.

| ![Mod1_lecture_02](/docs/images/lecture_screenshots/Mod1_lecture_02.png) |
|:---:|

### 1.2 - Introduction To FinFETs

FinFETs became necessary because planar MOS devices could no longer suppress short-channel effects at sub-30 nm gate lengths. By using a multi-gate 3D structure, FinFETs improved **electrostatics, variability, subthreshold swing, and drive current density**, while enabling lower $(V_{DD})$ operation. This combination extended CMOS scaling for a decade until the industry shift toward GAA nanosheets.


| ![Mod1_lecture_03](/docs/images/lecture_screenshots/Mod1_lecture_03.png) |
|:---:|
|![Mod1_lecture_04](/docs/images/lecture_screenshots/Mod1_lecture_04.png) |

#### 1.2.1 - Why FinFets ?
##### 1) Electrostatic Integrity and Short-Channel Effects (SCEs)
  - In planar MOSFETs, as the gate length $(L_g)$ scaled below ~30 nm, the gate lost control over the channel potential because the depletion regions of the source and drain began to overlap.  
  - This resulted in severe **drain-induced barrier lowering (DIBL)**, **threshold voltage $(V_T)$ roll-off**, and increased **subthreshold slope (SS)** (> 70–80 mV/dec, compared to the ideal 60 mV/dec).  
  - FinFETs, being double-gate or tri-gate structures, increase the gate-to-channel coupling by wrapping the gate around the fin, thereby suppressing SCEs and enabling continued $L_g$ scaling into the sub-20 nm regime.  

##### 2) Improved Subthreshold Swing and Leakage Control
  - Planar MOSFETs suffer from poor subthreshold slope due to weak gate coupling.  
  - FinFETs achieve **subthreshold swing closer to the Boltzmann limit (≈60 mV/dec at 300 K)** because the gate controls the channel from multiple sides.  
  - This translates to **significantly reduced off-state current $(I_{off})$**.<!--, enabling both high-performance (HP) and low-power (LP) product variants.  -->

##### 3) Enhanced Drive Current and Effective Channel Width
  - The fin geometry introduces a **3D channel** with effective width:  
  $W_{eff} = 2H_{fin} + W_{fin}$
  
  where $H_{fin}$ is the fin height and $W_{fin}$ is the fin width.  

  - By increasing fin height or using multiple fins in parallel, designers can boost the on-state drive current $(I_{on})$ **without increasing the footprint**, providing scalability in both performance and density.  

##### 4) Reduced Variability
  - Random dopant fluctuations (RDF) in planar devices created large $(V_T)$ variability because planar MOSFETs required heavy channel doping to control SCEs.  
  - FinFETs achieve electrostatic control **primarily through geometry (fin thickness $(T_{fin})$**, which allows for **undoped or lightly doped channels**, reducing RDF and improving device uniformity.  

##### 5) Lower Operating Voltage $(V_{DD})$ and Power Efficiency
  - With improved electrostatic control, FinFETs maintain performance at reduced supply voltages, enabling **dynamic power scaling $(P \propto C V^2 f)$**.  
  - Leakage suppression also reduces static power, a major contributor in advanced nodes.  

##### 6) Scalability Beyond Planar CMOS
  - FinFETs were manufacturable using existing CMOS process extensions (HKMG integration, strain engineering) while providing a **scaling path from 22 nm → 7 nm → 5 nm nodes**.  
  - They act as the evolutionary bridge toward **Gate-All-Around (GAA) nanosheet/nanowire FETs**, where the gate fully wraps around the channel for even stronger control.  

| ![Mod1_lecture_05](/docs/images/lecture_screenshots/Mod1_lecture_05.png) |
|:---:|
| ![Mod1_lecture_10](/docs/images/lecture_screenshots/Mod1_lecture_10.png) |

### 1.3 FEOL Innovations
#### 1.3.1 - CMOS Technology Inflection Points

|  | **Dennard Scaling Era (~1 µm to 32 nm)** |
|:---|:---|
| ~1 µm (1980s) – 180 nm (1999) | Supply voltage scaling enabled higher integration (Dennard scaling) |
| 130 nm (2000) | Introduction of Cu BEOL (copper interconnects). |
| 90 nm (2003) | Uniaxial strained Si for mobility boost. |
| 65 nm (2005) | eSiGe + low-k dielectrics. |
| 45 nm (2007) | Transition to high-k / metal gate (HKMG) (first HK-first, MG-last). |
| 32 nm (2009) | HKMG + raised source/drain, improving leakage and variability. |
|  | **Post-Dennard / New Device Architectures (22 nm onward)** |
|  22 nm (2012) | Shift to FinFETs (Tri-Gate transistors) for leakage control |
| 14 nm (2014)/ 10 nm (2016) | Multiple patterning (SADP, SAQP, LELELE) to continue scaling |
| 7 nm (2018) | EUV lithography adoption. |
| 5 nm (2020) | SiGe FinFET PMOS with EUV for better performance. |
| 3/2/1.4 nm (2023-2025) | Transition to Gate-All-Around (GAA) nanosheet/ nano-wire FETs. |
| Sub-1 nm (future) | Exploration of CFET (stacked devices), 2D materials (e.g., MoS₂), and higher-k dielectrics for ultimate scaling. |


#### 1.3.2 - Standard Cell Area Scaling

As process nodes continues to shrink, classical scaling vectors (like gate pitch) become increasingly challenging. Scaling boosters aid traditional scaling vectors through various modifications and enhancements to a process node. They may be part of the process technology flow itself or as part of the standard cell library as part of the design-technology co-optimization (DTCO). By combining scaling boosters with slightly less aggressive classical scaling vectors, a process node can achieve similar transistors density while keeping the process cost in check.

#### 1.3.2.1 - Track Reduction (Fin Depopulation in the context of FinFETs)
  - Is a technique for improving the density of the standard cell library by reducing the number of fins per FinFET transistor or the height of the active N or P region.  
  - By reducing the height of the active region, the number of tracks is reduced thereby reducing the height of the standard cell and ultimately increasing the transistor density of the chip.  
  - In the case of FinFET, fin depopulation results in energy reduction but also performance reduction.

| ![Mod1_lecture_08](/docs/images/lecture_screenshots/Mod1_lecture_08.png) |
|:---:|

| ![Mod1_lecture_09](/docs/images/lecture_screenshots/Mod1_lecture_09.png) |
|:---:|

#### 1.3.2.2 - Single Diffusion Break (SDB)
  - Cell boundaries were traditionally padded with an additional dummy gate right after the active diffusion regions, at fin ends, for better cell control. As node scaling continued, due to cell height reduction, the portion of the area that makes up the dummy gate grew.  
  - Single Dummy Gate (SDG) or Single Diffusion Break (SDB) is a process enhancement technique that eliminates the extra padding around the cell edge when packaging multiple cells, thereby reducing the effective transistor density at the block and macro level.

#### 1.3.2.3 - Contact Over Active Gate (COAG)
  - Typically, the area between the end of the nMOS and pMOS devices is used as the gate contact hit location.  
  - Self-aligned Contact Over Active Gate (COAG) is a process enhancement technique that eliminates the need to land the contact outside of the active gate, allowing the gate contact to land directly over the active gate, thereby reducing the amount of space the end-to-end (ETE) spacing between devices.

#### 1.3.2.4 - Buried Power Rail (BPR)
  - Power rails (VDD, VSS) are buried below the active device layer instead of occupying tracks in the standard cell.  
  - Traditionally, power rails run in the first metal layers (M0/M1). By moving them below the device layer, the routing tracks in BEOL are freed for signal routing.  
  - BPR helps to increase the routing resources in standard cells leading to higher logic density, and reduces the cell height enabling tighter standard-cell libraries.  
  It also helps lower the local IR drop by providing a shorter path for VDD/VSS distribution to the devices.

#### 1.3.3 - Parasitic Resistance And Capacitance

As CMOS technology continues to scale beyond the planar MOSFET era into FinFET, Gate-All-Around FETs (GAAFETs), and Complementary FETs (CFETs), device performance is increasingly impacted by **parasitic resistance $(R_{EXT})$** and **parasitic capacitance $(C_{par})$**. These parasitics, once secondary, now play a first-order role in determining drive current, delay, and energy efficiency at advanced nodes.

##### 1.3.3.1 Parasitic Resistance

| ![Mod1_lecture_11](/docs/images/lecture_screenshots/Mod1_lecture_11.png) |
|:---|

| Planar MOSFETs | FinFETs | GAAFET | CFET |
|:---|:---|:---|:---|
| <ul> <li>**Contact width $(W_C)$** is nearly equal to the **Gate width $(W_G)$**: <br>  $\frac{W_C}{W_G} \sim 1$ </li><li>Ratio of external to channel resistance: <br>  $\frac{R_{EXT}}{R_{ch}} < 1$</li><li> Channel resistance dominates; external resistance is relatively minor.</li> </ul> | <ul> <li>Conduction occurs through vertical fins, with current spreading across sidewalls.</li><li>Effective width ratio: <br>  $\frac{W_C}{W_G} \approx \frac{P}{(2H_f + D_f)} \sim \frac{1}{3}$</li><li>Ratio of resistances: <br>  $\frac{R_{EXT}}{R_{ch}} \sim 1$</li><li>External resistance becomes comparable to channel resistance.</li> </ul> | <ul> <li>In nanosheet/nanowire GAAFETs, the contact width per effective gate width decreases further: <br>  $\frac{W_C}{W_G} \sim \frac{1}{6}$</li><li>$\frac{R_{EXT}}{R_{ch}} \sim 3$</li><li>External resistance dominates device performance.</li> </ul> | <ul> <li>CFETs (stacked N- and P-FETs) inherit nanosheet-like geometries with: <br>  $\frac{R_{EXT}}{R_{ch}} \sim 3$</li><li>Parasitic resistance remains a major limiting factor.</li> </ul> |


| ![Mod1_lecture_12](/docs/images/lecture_screenshots/Mod1_lecture_12.png) |
|:---|

| **$\mathbf{R_{EXT}}$ Components** |
|:---|
| **$\mathbf{R_{FEOL}}$**: Front-End-Of-Line resistance from the source/drain diffusion region up to the silicide or first contact. <br> <ol> <li>$R_{EPI}$: Epitaxial resistance in the raised source/drain epitaxy.</li> </ol> |
| **$\mathbf{R_C}$**: Contact resistance between the silicide (or epitaxial region) and the contact metal. <br> Dominant component at advanced nodes. <br> Determined by: <ul> <li> Schottky barrier height (SBH)</li><li>Interface quality</li><li>Doping at the contact interface.</li> </ul> |
| **$\mathbf{R_{MOL}}$**: Middle-Of-Line resistance - inludes resistance of the local interconnect stack connecting the contact to higher-level metal. <ol> <li>$R_{TS}$: Transistor Spacer resistance - resistance of the narrow constriction where current passes under the spacer, between the gate edge and the raised source/drain.</li><li>$R_{CA-TS}$: contribution of the contact area to transistor spacer path.</li><li>$R_{CA}$: Contact area resistance</li> </ol> |
| **$\mathbf{R_{BEOL}}$**: Back-End-Of-Line resistance - resistance from the global interconnect stack (Cu/Co/Ru wires, vias, etc.) including $R_{CA-BEOL}$. |

Measurements of the contribution by each component of the parasitic resistances show that:
  - In NFET: Contact resistance, $R_C$ dominates (~63% initially) which could be improved to within 10%-40%.
  - In PFET: More evenly distributed between $R_C$ and $R_{EPI}$.

Improvement strategies:
  - Lower the Schottky Barrier Height (SBH)
  - High source/drain doping near the contacts

##### 1.3.3.2 Parasitic Capacitance

| ![Mod1_lecture_13](/docs/images/lecture_screenshots/Mod1_lecture_13.png) |
|:---|

As nodes shrink, the **effective capacitance (C_eff)** becomes dominated by parasitics:
  - **C_of**: Overlap/fringe capacitance
  - **C_pc-ca**: Contact-to-channel capacitance
- Node evolution:
  - **22 nm**: C_g ~ 56%, parasitics minor.
  - **7 nm**: Parasitics dominate (~85%), C_g ~ 15%.

Spacer Engineering:
  - Spacer materials strongly influence parasitic capacitance.
  - Low-k spacers reduce parasitic capacitance (SiN > SiBCN > SiOCN > SiCO)
  - Ultimately **Air spacers**


#### 1.3.4 - Device Scaling
As scaling approaches sub-5 nm gate lengths, conventional transistors face fundamental limits.  
Challenges for sub-5nm gate length scaling:
  - Direct source-to-drain tunneling increases drastically at ultra-short channels:
    - Need for high effective mass
  - Electrostatics degrade due to surface roughness and thickness variations:
    - Need for uniform atomically thin materials
  - $C_D$ high relative to $C_{OX}$ --> higher Subthreshold Slope
    - Need for low in-plane dielectric constant

| ![Mod1_lecture_15](/docs/images/lecture_screenshots/Mod1_lecture_15.png) |
|:---:|

This forces us to look for new channel materials - where **Transition Metal Dichalcogenides (TMDs)** offer a promising pathway in the sub-5nm regime.

Layered TMD semiconductor materials such as MoS₂, WS₂, MoTe₂, and WSe₂ offer these properties of atomically uniform thickness, higher effective mass and a tunable bandgap

**<U>Scaling Benefits:</U>**
  - Suppressed source-to-drain tunneling: Dual-gate MoS₂ MOSFETs show up to 100× reduction in tunneling leakage compared to Si, due to larger bandgap and higher m*.
  - Ultra-short channel feasibility: MoS₂-based devices have demonstrated gate lengths down to 1 nm (using a carbon nanotube gate).
  - Energy efficiency: Reduced leakage allows large energy savings in ultra-low-power electronics.
  - Excellent electrostatics: Near-ideal subthreshold slope (~65 mV/dec) and high Ion/Ioff ratios (~10⁶) have been demonstrated.

**<U>Device Demonstrations:</U>**
| **1 nm MoS₂ transistor** <br> ![Mod1_lecture_17](/docs/images/lecture_screenshots/Mod1_lecture_17.png) | ![Mod1_lecture_18](/docs/images/lecture_screenshots/Mod1_lecture_18.png) |
|:---:|:---:|
| **All 2D MOSFET** <br> ![Mod1_lecture_19](/docs/images/lecture_screenshots/Mod1_lecture_19.png) | ![Mod1_lecture_20](/docs/images/lecture_screenshots/Mod1_lecture_20.png) |
| **TMDs on 3D surfaces** <br> ![Mod1_lecture_22](/docs/images/lecture_screenshots/Mod1_lecture_22.png) | ![Mod1_lecture_23](/docs/images/lecture_screenshots/Mod1_lecture_23.png) |


#### 1.3.5 - 3D-Structures

CFET, or Complementary FET, is a future transistor architecture that stacks NMOS and PMOS transistors vertically on top of each other to increase transistor density and reduce chip area. The CFET architecture is an evolution of a Gate-All-Around architecture, where the NFET and PFET are stacked vertically rather than side by side.

Two CFET manufacturing integration schemes have been proposed – one that grows the PFET and NFET together in a **monolithic** manner and the other that grows them **sequentially**. The monolithic approach offers better performance and lower cost. However, extremely high aspect ratio (HAR) etching is needed for monolithic integration. The sequential approach allows more flexibility in NFET and PFET channel materials. However, a very accurate NFET-PFET alignment is needed using sequential integration.

| ![Mod1_lecture_24](/docs/images/lecture_screenshots/Mod1_lecture_24.png) |
|:---|
| _**Ref:**_ [Monolithic 3D CMOS Using Layered Semiconductors](https://advanced.onlinelibrary.wiley.com/doi/abs/10.1002/adma.201505113) |

_**Quoting directly from the above paper:**_  
_"In all CMOS logic circuits, a pair of NMOS & PMOS transistors shares the same gate that accepts an input signal, and NMOS & PMOS transistors always exist in pairs. Taking inverter as an example, NMOS & PMOS transistors can be folded on top of each other along the line of symmetry (M–N) so that each pair of these transistors shares a common gate [Figure (d)]. The source and drain contacts for NMOS and PMOS transistors cannot be always shared and hence should be electrically isolated from each other and connected using metal lines as required. The resulting unit cell for 3D CMOS has an NMOS and a PMOS stacked on top of each other sharing a common gate metal and the source and drain contacts for the two transistors are electrically isolated as shown in Figure (b). Additional layers of logic gates and memory can be stacked over this layer separated with a thick dielectric called the interlayer dielectric to further increase the integration density."_

**References on CFET:**  
1) [https://www.imec-int.com/en/articles/imec-puts-complementary-fet-cfet-logic-technology-roadmap](https://www.imec-int.com/en/articles/imec-puts-complementary-fet-cfet-logic-technology-roadmap)
2) [https://newsroom.lamresearch.com/understanding-cfets-transistor-architecture](https://newsroom.lamresearch.com/understanding-cfets-transistor-architecture)

### 1.4 - BEOL Innovations
Back-End-Of-Line (BEOL) interconnects — responsible for signal routing and power delivery — have become a critical performance bottleneck. While transistor performance has continued to scale, interconnect resistance and capacitance scaling lags behind, leading to delay, energy, and reliability issues.  
Innovations in BEOL are therefore essential to sustain system-level scaling.  

| ![Mod1_lecture_27](/docs/images/lecture_screenshots/Mod1_lecture_27.png) |
|:---|

#### 1.4.1 - Extending Copper Interconnects
At reduced pitches (≤ 28 nm), Cu resistivity rises due to size effects, scattering, and barrier/liner overheads.

Barrier and via metal optimization through Selective barrier deposition reduces via resistance by up to 50%, allowing Cu interconnects to remain viable down to ~3 nm nodes before a transition to alternative metals is required.

#### 1.4.2 - Transition to Non-Cu Metals

As Cu scaling saturates, alternative metals like Ru, Co, Mo, Rh, Ir are explored.

Advantages:
  - Improved electromigration (EM) reliability.
  - Lower resisitivities and low electron scattering at small interconnect dimensions.


#### 1.4.3 - Back-Side Power Delivery Network (BS-PDN)
In traditional front-side PDN (FS-PDN), power and signals share BEOL layers, leading to IR drop and routing congestion.  
In Back-side PDN (BS-PDN), power delivery vias are routed through the wafer backside
  - Reduction in IR-drop and power integrity.
  - As the power delivery layers are separated, this frees up routing resources on the front-side metal layers for signal routing leading to reduced congestion and improved parasitic RC delays and thus performance.
  - Helps decrease standard cell area by allowing tighter standard cell scaling (from 6-track to 5-track libraries).

| ![Mod1_lecture_30](/docs/images/lecture_screenshots/Mod1_lecture_30.png) |
|:---|


_________________________________________________________________________________________________________  
