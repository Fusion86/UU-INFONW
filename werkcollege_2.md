# Bus Interconnection

1.  1. 32 bit \* 100 000 000 hz = 3 200 000 000 bps = 3.2 Gbps
    2.

# Byte Sizes – order according to size (from largest to smallest; descending order)

1. a full-HD bitmap image (1920 x 1080 pixels, 3 colour channels)
2. a 3 minute raw audio recording (samples at 256 Kbit / sec)
3. a 20 second raw video stream (audio sampled at 96Kbit / sec, image resolution 720 x 576
   pixels; frame rate of 25 images / sec; 3 colour channels)
4. A finger CT scan (raw format): 100 x 100 x 100 voxels (→ volume pixels); monochromatic; 16-bits per pixel intensity

## Sizes

Assuming no file headers and stuff for simplicity.

1. `1920 * 1080 * 3 / 1000` = 6220,8 KB
2. `3 * 60 * 256 000 / 8 / 1000` = 5760 KB
3. video: `720 * 576 * 3 * 25 * 20 / 1000` = 622 080 KB
   audio: `96 000 * 20 / 8 / 1000` = 240 KB
   total: 622 320 KB
4. `100 * 100 * 100 * (16/8)` = 2 000 KB

Order large to small: 3 1 2 4

These size do not match up with 'familiar' file formats because we use compression almost everywhere.

## Memory Types

volatile memory is memory which loses all its data on poweroff.  
static ram is fast and expensive, it uses circuits (flipflops?) to store data.  
dynamic ram is cheaper and slower, it uses capacitors to store data. these capacitors need to be refreshed regularly to retain their data.

## Memory access – read/write

1. The address bus is used to request data from a specific device (e.g. a specific ram address). The data bus is used to transmit the actual data.
2. idk?
3. todo...

## Memory Organisation & Types

1. 1 byte and 16 in one line?

-- TODO: Ask what the difference is between segmentation and paging, and whether they are used together? --

## Memory – Segmentation

1. For protection?
2. Code, Data
3. total memory size: 1 GB
   remaining bit: segment register to select which table, global or local???
   selector: segment description table selector
   local address: the address of the virtual memory (which is added to the `segmentTable[selector]` address)
   how big physical: `2^24 / 1024 / 1024` = 24 MB?
   how big segment: `2^16 / 1024` = 64 KB?

## Memory - Paging

1. 
