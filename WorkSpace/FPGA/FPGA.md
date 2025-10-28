

### Responsed Jobs for FPGA

#### DDR Integration jobs

##### SERDES integration for In-house DDR3 SDCTRL

* The first begin of this job is to integrate the in-house SDCTRL to let it can be verified in FPGA enviromnent. Therefore, the first job is first to solve the FPGA translate problem from V7 to V9, we start to layout another DDR3 daughter board, but the data access still wrong, the final cause we thought is the new-layout DDR3 daughter board which the signal wire connections are not balanced. The constraints can not meet the real situation. Therefore, we start the think about a method to solve this problem by by clock phase (90-180-270-360 degrees) control way. the first trial version is to use the SERDES to control the DDR3 PHY signals to adjust the timing in phase level to overcome this problem.

* In original PHY design, we control the all the phase from DDR3 interface to fine-tune the timing, Finally, the implemented design can be run at 108MHz in DDR3 interface, the reason can not be enhanced because the timing buttleneck is occured in In-house DDR Controller. Therefore, we start to think about the next generation improvement to solve this problem

##### MIG DDR4 PHY integration

* We note that we can generated with only-phy interface to integrated in-house SDCTRL. Therefore, 

#### HDMI Integration Jobs

#### HDMI PHY + In-house HDMI Tx integration

* The original HDMI interface connects to a _________ which the connected ways is GPIO, and it can only runs at 27MHz, which means if the resolution is higher than 480P, it can not be normally verified with a standard speed, which can not be achieve the real situation. 

* In this job, The HDMI PHY has been integrated into you SOC system, the IBERT tests are both PASS.
The whole experimental environment are showns as follows

* V9
The FPGA test board are based on XCVU9P-L2FSGD2104E (https://talentpros.com.tw/tps-8-series-lite)
* HDMI daughter board
https://www.mouser.com/new/texas-instruments/ti-tdp158rsbevm-evaluation-module/


* HDMI Analyzer

Finally, the HDMI Tx can runs at 74.25MHz, compared with the original speed with 27MHz, which has extreamly improvement.
Totally, the whole system can run at 74.25MHz with 720P60. The following images shows the results, the test patterns comes from the internal BIST mode in in-house HDMI Tx. which shows the iamge can be normally captured with correct DTG timing.