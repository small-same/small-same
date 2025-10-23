### Brief Introduction for DDFCH Implementation 

This design implementes the integration changes for the **Data Fetching (DDFCH)** module within the **4K Display System**, from DRAM and Frame Buffer Decompression (FBD) IPs.

<img src="overview.png" alt="Logo" width="1000">

1. It supports the original 2K solution with original path, and FBD path for 4K resolution, which translate the image format to linear to VSCL format (4x1 or 4x2 pixel data).
2. The memory pools which supports frame and field mode which stores the pre-fetched decompressed Luma/Chroma pixels, which provides a dual read/write modes tp save memory usage about 50%, compared with traditional ping-pong buffering, and provide faster response time for writing (quarter data of each four lines)
3. Provides Decimation Function (Down Scaling) to write back the pixel data to DRAM.

About Point 2, here gives an brief example to show how the SRAM POOL works to translate an 4x4 write ordering to 4x1 ordering. There is a 32x8 pixels images, (x,y) means pixel position in an image, total 16 cycles data with 4x4 blocks. The write ordering is an 4x4 block with roster scan, as the following figure

<img src="write_ordering_example.png" alt="write_ordering" width="1000">

* The following image shows how to use the two modes to complete the circule process. for an 4x1 output data, which means the minimum using banks is 4, each SRAM only has address 0 and 1. This brief example shows how to control the address/bank/wen bits to handle this situation.

<img src="sram_pool_example.gif" alt="sram_pool_example" width="500">

