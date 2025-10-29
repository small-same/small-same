

### Responsed Jobs for FPGA

#### DDR Integration jobs

* The whole FPGA jobs are used [XCVU9P-L2FSGD2104E](https://talentpros.com.tw/tps-8-series-lite), and implemented by [VIVADO](https://www.xilinx.com/support/download.html). The main reason is for our 4K IC verification, the resource of original FGPA board [HAPS-70](https://news.synopsys.com/2013-12-16-Synopsys-Extends-HAPS-70-Prototyping-Family-with-New-Solution-Optimized-for-IP-and-Subsystems) can not handle the the new 4K IC, therefore, our jobs to ports the 4K system into the new FPGA platform.

##### SERDES integration for In-house DDR3 SDCTRL

* For the new FPGA V9 platform, we layouts another DDR3 daughter board. Somehow, after testing, but the data access still has problem, the CPU still can not recieve the correct data. We notes that the reason is the signal integerity of DDR3 interface which has bad signal balance. Therefore, to solve this problem from FPGA, we have to give a dynamically settings to setup the delays from each DDR3 pins to dynamically tests the data correctness. Therefore, we added serveral SERDES in data and control signals, and the RTL in PHY can handle the parllel to serial problem from the clock ratio 4:1 problem. Finally, by controlling clock phase (90-180-270-360 degrees), the DDR3 PHY signals to adjust the timing in phase level to overcome this problem.

* In this PHY design, all the phase from DDR3 interface can gives an fine-tune the timing way. The implemented design can be run at 108MHz data rate in DDR3 interface, the reason can not be enhanced because the timing buttleneck is occured in In-house DDR Controller. Therefore, we start to think about the next generation improvement to solve this problem.

##### MIG DDR4 PHY integration

* We note that we can generated with only-phy IPs to integrated in-house SDCTRL. It gives us three interface for connection, Considering the DDR4 interface can not be directly connect to the in-house SDCTRL, Therefore, we start to connect the interface between the [USER interface, PG150](https://docs.amd.com/r/en-US/pg150-ultrascale-memory-ip/User-Interface?tocId=kLdS~zIRXPqmOCWQcjY~7wfrom). However, this project can not be completed before I leave.

#### HDMI Integration Jobs

#### HDMI PHY + In-house HDMI Tx integration

* The original HDMI interface connects to a [ADV7842/ADV7511 Video Evaluation Board](https://www.analog.com/media/en/technical-documentation/user-guides/UG-235.pdf) which connects the FPGA IOs. For example, HDMI interface connects three channels and sync signals, which over 30 pins which need to connect to this board. it leeds the speed can not be enhanced, and it can only runs at 27MHz, which means if the resolution is higher than 480P, it can not be normally verified with a standard speed, which can not be achieve the real situation. 

* The improving way for this jobs is try to connect the original HDMI ports from 
* PG230

* In this futhrer job, the first is to port the example design of PHY, and be integrated into you SOC system, the IBERT tests are both PASS.
The whole experimental environment are showns as follows

<img src="env.png" alt="RESULT" width="350">

* HDMI Redriver
(https://www.ti.com/tool/TDP158RSBEVM)


* HDMI Analyzer (https://www.teledynelecroy.com/protocolanalyzer/quantumdata980.aspx)


Finally, the HDMI Tx can runs at 74.25MHz, compared with the original speed with 27MHz, which has extreamly improvement.
Totally, the whole system can run at 74.25MHz with 720P60. The following images shows the results, the test patterns comes from the internal BIST mode in in-house HDMI Tx. which shows the iamge can be normally captured with correct DTG timing.

<img src="brief_result.jpg" alt="RESULT" width="750">