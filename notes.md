# Some notes

Whenever a course note is inserted it means that it is copied 1:1 from the worksheet without fact/logic checking etc. I intend to replace all these parts with human-speak.

## Bus Interconnection

Keep in mind that (unless noted otherwise) all answers are in **B**ytes per second (big B) and not **b**its per seconds (small b).

### What is the throughput of a 32 address/data bus at 100MHz?

We only look at the throughput of the data bus, because the address bus is not used for the actual data transfer (only used to know where to read the data from).

```python
freq = 100 * 1000 * 1000 # 100 MHz to Hz
size = 32 / 8 # 32 bits to bytes

# Devide by 1_000_000 to convert from bps to MBps
freq * size = 400 # MBps
```

### At what frequency does a 64 bit bus need to run to achieve a throughput of 12.4 GBps?

```python
tp = 12.4 * 1000 * 1000 * 1000 # 12.4 GBps throughput

# Divide twice by 1000 (base -> kilo -> mega)
tp / 8 / 1000 / 1000 = 1550 # 1500 MHz
```

## What is the throughput of a 32 bit databus and a 64 bit address bus operating at 133 MHz?

```python
bus_size = min(32, 64) # See notes
bits = bus_size / 8 # 32 bits to bytes
freq = 133 * 1000 * 1000 # 133 MHz to Hz

bits * freq / 1000 / 1000 = 532 # MBps
```

**Course note**

Comment ‘real throughput’: it orients itself on the lowest-width bus line (i.e. data or address). If both widths are the same, then this is no problem. If the data bus is smaller, we can transmit less information at each clock – even if the address bus is very large. If the address bus was smaller (e.g. we operate with 64-bit addresses while the address bus is only 32-bit wide), we need 2 bus clocks to transmit 1 address, so we only can transmit 1 data item over the data bus back to the requesting component for every 2 clocks of the bus (→ we need a whole 64-bit address to retrieve the data). Thus, in that case, the bandwidth is limited by the address bus width, not the data bus width. This definition does go against manufacturer claims, which are basing their bandwidth numbers on the data bus exclusively (to advertise greater speeds). They omit the fact that their device/components would not receive addresses at the same speed, which ‘starves’ the bus transmission. This can obviously also go vice-versa: the address bus is very wide, the data bus is smaller, hence data transmission is crippled by the data bus, but business people are advertising transmission speed with the address bus.

## Memory – Segmentation

## Which segments do we have?

- Code (instruction segment)
- Data segment
- Stack segment

## Why do we segment the memory?

When multi threading all threads share the same code and data stack. Each thread has its own stack segment.

**Course note**

data protection; allow multiple programs to run in an alternating fashion by sharing
instruction segments → one program runs at a time, so only one code segment needs to be
active.

## Using segment descriptors

### What is the total memory size addressable with a 30 bit virtual address?

```python
# Divide three times by 1000 (bytes -> kbytes -> mbytes -> gbytes)
2 ^ 30 / 1024 / 1024 / 1024 = 1 # GB
```

Note: it does not matter that this is a virtual address, the only important bit is the bit count.

### Inside a 30 bit virtual adres we have 13 MSBs which are the selector and 16 LSB which are the local address. What is the last bit used for?

The remaining bit is the table selector. With 1 bit we can select `2^1 = 2` different tables.

Selector = selects the individual segment to-be-loaded into memory
Local address = offset within the given segment

The 13 selector bits give access to `2^13 = 8192` segment table entries.

### The base address space (and this the physical address space) is 24 bits. How large is the physical memory?

```python
2^24 / 1024 / 1024 = 16 # MB
```

### The local address is 16 bits. How large is each memory segment?

```python
2^16 / 1024 = 64 # KB
```

Note: this assumes that each memory segment is indeed exactly as large as the local address allows it to be. I don't know if this is always the case.

### Why do we have 32 times more segment descriptor entries than we have unique segments entries.

13 bit selector = 8192 entries in the descriptor table.
(24 bit address - 16 bit local address) = 8 bit segment part = 256 entries

8192 / 256 = 32 times more segment descriptor entries.

**Course notes**

We have overlapping segments, for example: if the total code segment is 12 KB, then this can be filled by 6 different 2KB segments, or 3x 4KB segments, or 4x 3 KB segments. Each of those segments exist – they just don’t uniquely need to fit into a
whole segment block. Also, individual segments do not need to be exactly 64KB large – they are theoretically, but some segments can be smaller. This happens particularly for data segments. The only segment that is nearly-uniform is the stack segment, because
it’s maximum size needs to be defined by the program or the operating system. Because of these irregularities in segment sizes, the segment descriptor needs to store the segment size.
In terms of the two tables in the example, we can occupy each segment either with ‘data’ or with ‘code’ - therefore, there may be segment descriptor duplicates, where a segment descriptor is in the ‘data segment table’ and the ‘code segment table’. In this example from the book though, one table stores global information and one stores local information (information here equals variable).

## Memory - Paging

### What is the purpose of memory paging?

Allows your virtual memory to be larger than the physical memory size.

### What is a page table?

**Course note**

A page table maps the page number code (encoded in the page number segment of the virtual address) into an actual page number than can be referenced in the system. It hence provides the base for the page offset (local address section) of the virtual address

### What is a page table directory?

**Course note**
Page table directory: a list of all available pages in the system, together with their access rights (read/write), protection etc.

## CPU – Layout

### What's the purpose of the control unit

**Course note**

- control the instruction flow
- define CPU frequency / speed
- process interrupts
- decode instructions
- convert instruction byte codes into operation signals
- send operation / command signals to the execution components (e.g. ALU)
- access external bus
- request & retrieve memory information;
