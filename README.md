
## Contact

* **Name:** Jerry Chang (張宗賢)
* **Email:** smallsame0816@gmail.com
* **Mobile:** +886 929939383

---

## Self Introduction

I have about **9 years of work experience in digital IC design**. My major responsibilities revolve around **SoC (System on Chip)**, including **IP design and integration** (DISPLAY – DDFCH, and TZMA), **IP verification** (verification plan and pattern writing), and **flow/utility development** (PTGreper and clock reset gen). Furthermore, regarding the front-end flow, I also have experience with **MBIST insertion** (Tessent), **Formal verification** (R2R, R2PRE, PRE2POST), and **timing closure**.

---

## Work Experience

### AVALINK - Hsinchu, Taiwan
**Senior Digital IC Engineer** | May 2019 – Oct. 2025

<details close>
  <summary>Details</summary>
   
* **RTL Design - DISPLAY 4K System**
    * [DDFCH](https://github.com/small-same/small-same/blob/main/WorkSpace/DDFCH.md)
      * Designed and optimized Data Fetching from DRAM IP, enhancing data throughput.
      * Developed Rotated SRAM design, achieving 50% memory usage saving, compared ping-pong buffering, through efficient block-to-linear ordering swap.
      * Implemented Display Cropping Functions with the integration of frame buffer decompression, achieving target performance.
    * **TZMA** 
      * Designed Trust Zone Memory Access IP, integrating with crypto engine to secure DRAM access, ensuring robust system security.
      * Developed Register Control for Secure/Non-Secure Master with Trust-Zone Access, improving system partition security.
* **Display Function Verification**
    * Developed comprehensive verification test plans and patterns, No functional fault happens at first cut tapeout.
    * Response FPGA emulation to validate display functionalities and accelerate pre-silicon debugging.
* **FPGA Implementation & Integration**
    * Implemention Flow on Xilinx V9 with VIVADO, meeting stringent performance targets.
    * Gained extensive integration experience with VIVADO IPs, including Serdes, MIG DDR4, and HDMI Tx PHY.
* **Project Experience with Tapout IC**
    * Contributed to the successful tape-out of SFH980 – a 4K setup-box IC with integrated In-house FBD (SMIC 40nm).
    * Involved in SFH821 – a 2K setup-box IC with 10-bit Coder (SMIC 40nm).
    * Participated in SFH826 – a 2K setup-box IC, leading the effort to fix critical issues from SFH821 (SMIC 40nm).


</details>

### Holtek Semiconductor - Hsinchu, Taiwan
**Digital IC Engineer** | Feb. 2018 – April 2019

<details close>
  <summary>Details</summary>

* **Functional Verification (Keil-C based)**: Functional verification for critical IP blocks including **Bus matrix**, **Test mode**, **DMA function**, and **in-house MBIST mode**.
* **RTL Integration**: Successfully integrated **BLE IP with specific test modes** into larger SoC designs, ensuring seamless functionality and adherence to specifications.
* **Front-End Flow Ownership**: Performed **Logic Equivalency Checking (LEC)** for entire chips, comparing R2R, R2G, G2G to guarantee design integrity.
* **Functional ECO Execution**: Has experience for Functional ECOs. 
* Script writing for **Front-end Flow Development**
    * Developed Perl/Tcl scripts for automated PrimeTime information extraction and analysis.
    * Conducted in-depth clock/data path analysis to identify and resolve clock tree balance issues, ensuring timing closure.
    * Buffer/double-Inverter usage calculation, optimizing gate-level netlist quality.
    * Summarized timing closure status for MRMC (TMS/WMS), providing critical insights for tape-out decisions.
* **Tape-out Project Contribution**: Contributed to the successful tape-out of a **Cortex-M3 + Integrated BLE SoC** on **UMC 28nm** process technology.

</details>   



### Montage Technology - Hsinchu, Taiwan
**Digital IC Engineer** | Apr. 2016 – Jan. 2018

<details close>
  <summary>Details</summary>

* **IP Design & Automation**:
    * Developed an **automated RTL generator for Clock/Reset Generation (clock reset gen)**
    * UART IP
* **Front-End Flow Management**:
    * Managed **MBIST (Memory Built-In Self-Test) insertion flow** from IP-level to top-level using **Tessent**.
    * Executed **Logic Equivalency Checking (LEC)** for entire chip designs (RTL to post-layout netlist) to verify design equivalence.
    * Performed **Manual Functional ECOs**

* **Tape-out Project Contribution**: Played a key role in the tape-out of the **Panther WIFI SOC** (fabricated on **SMIC 40nm** process technology).

</details>   

---

## Skills

* **Programming language** – Verilog, System Verilog, Perl, Tcl, C, C#
* **Front-end tools** – Tessent, Design Compiler/Genus, Primetime, Conformal/Formality, irun
* **Application framework/Tools** – Keil µVision, Arm-linux Toolchain
* **Language for algorithm development** – MATLAB
* **FPGA tools** – Vivado

---

## Education

### National Cheng-Kung University - Tainan, Taiwan

**Ph.D., Electrical Engineering** | Sep. 2010 – Feb. 2016

### Shu-Te University - Kaohsiung, Taiwan

**M.S., Computer Science** | Sep. 2007 – Jun. 2009

---

## PhD. Research Fields

* Speech/Audio Coding
* Algorithm/Architecture development for fixed-point arithmetic

---

## Publications

<details close>
  <summary>Details</summary>
  
### Journals

1.  Chung-Hsien Chang, Bo-Wei Chen, Shi-Huang Chen, Jhing-Fa Wang, and Yu-Hao Chiu, "Low-Complexity Hardware Design for Fast Solving LSPs With Coordinated Polynomial Solution," **IEEE Trans. on VLSI**, vol.23, no.2, pp.230-243, Feb. 2015.
2.  Chung-Hsien Chang, Shi-Huang Chen, Bo-Wei Chen, Wen Ji, K. Bharanitharan, and Jhing-Fa Wang, “Fixed-point Computing Element Design for Transcendental Functions and Primary Operations in Speech Processing”, **IEEE Trans. on VLSI**, vol.24, no. 2, pp. 1993-1997, May 2016.
3.  Chung-Hsien Chang, Bo-Wei Chen, Shi-Huang Chen, Jhing-Fa Wang, and Wei Jen, “Low-complexity Audio CODEC for Resource-scarce Embedded System with Fixed-point Arithmetic”, **JCIE**. vol. 39, no. 3, pp. 303-314, 2016.

### Conferences

1.  Chung-Hsien Chang, Po-Chuan Lin, Yu-Hao Chiu, Jhing-Fa Wang, and Ta-Wen Kuan, “A low-complexity sound recording system for elderly security in home-care system”, in Proc. **International Conference on Orange Technologies**, Xian, China, 2014, Sep. 20-23, pp. 185-188. (Algorithm Design)
2.  Chung-Hsien Chang, Po-Chuan Lin, Ta-Wen Kuan, Jhing-Fa Wang, Jing-Min Chen, and Jaw-Shyang Wu, “Multi-level Smile Intensity Measuring Based on Mouth-Corner Features for Happiness Detection,” in Proc. **International Conference on Orange Technologies**, Xian, China, 2014, Sep. 20-23, pp. 181-184. (Algorithm-level Design)
3.  Chung-Hsien Chang, Shi-Huang Chen, Bo-Wei Chen, Chih-Hsiang Peng, and Jhing-Fa Wang, "High-Efficient Hardware Design Based on Enhanced Tschirnhaus Transform for Solving the LSPs," in Proc. **IEEE International Symposium on Circuits & Systems**, Beijing, China, 2013, May 19-23, pp. 1440-1443. (Digital System on FPGA)
4.  Chung-Hsien Chang, Shi-Huang Chen, Bo-Wei Chen, and Jhing-Fa Wang, "A Division-Free Algorithm for Fixed-Point Power Exponential Function in Embedded System," in Proc. **International Conference on Orange Technologies**, Tainan, Taiwan, 2013, Mar. 12-16, 223-226. (Algorithm-level Design)
5.  Chung-Hsien Chang, Shi-Huang Chen, and Jhing-Fa Wang, "Fast Macro-block Selection Algorithm Using 2-D Haar Wavelet Features for H.264 Video Codec," in Proc. **International Conference on Genetic and Evolutionary Computing**, Shenzhen, China, 2010, Dec. 13-15, pp. 610-613.
6.  Shi-Huang Chen, Chung-Hsien Chang, and Shih-Yin Yu, “Fast Wavelet-based Macro-block Selection Algorithm for H.264 Video Codec,” **The International Multi Conference of Engineers and Computer Scientists**, pp. 421-424, Mar. 19-21, 2008, Hong Kong. (Algorithm-level Design, Best Paper Award)

</details>   
