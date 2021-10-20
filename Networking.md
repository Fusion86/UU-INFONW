# Networking Notes

## TODO

- Circuitswitching
- Packetswitching
- FDM/TDM
- Layers (NOT the OSI layer, we only use 5 layers)
- Stop-and-wait vs Pipelining/Sliding-window

## Connection types

### Connection-oriented

Creates a connection before sending data. Has 3 steps.

1. Create connection
2. Send/receive data
3. Close connection

Examples:

- Phone
- TCP

### Connection-less

Each message is sent without making a connection.

Examples:

- A letter
- UDP

## Transport Protocols

### TCP (Transmission Control Protocol)

- Reliable protocol
- Guaranteed order of delivery
- Can detect errors
- Connection-oriented

### UDP (User Datagram Protocol)

- No 'guaranteed' reliability
- "Best effort", aka it might reach it's destination, or not.
- No guaranteed order of delivery

### IP (Internet Protocol)

IP is used to route the TCP and UDP data through the internet.

### Multiplexing

"In telecommunications and computer networks, multiplexing is a method by which multiple signals are combined into one signal over a shared medium. The aim is to share a scarce resource."

Examples:

- Multiple phone calls over a single line
- Multiple radio or tv channels over coax

### FDM (Frequency-Division Multiplexing)

Data is sent at the same time, but on different frequencies.
Examples:

- Radio 1 on 98.8 MHz
- Radio M on 93.1 MHz

![](https://www.rfwireless-world.com/images/FDM-frequency%20division%20multiplexing.jpg)

### TDM (Time-Division Multiplexing)

Data is sent in alternating chunks within the same frequency.

![](https://www.rfwireless-world.com/images/TDM-time%20division%20multiplexing.jpg)

### FDM and TDM

You can also combine FDM and TDM. An example is the GSM network, where there are multiple channels which allow for multiple phone calls within a channel.

![](https://i.imgur.com/pMIhDW7.png)

### Statistical time-division multiplexing

Bij statistische multiplexing zijn kanalen naar behoefte toegewezen, er is geen vaste volgorde en geen vaste grootte.

### Circuit switching/multiplexing

Pros:

- Shared connection medium
- Guaranteed bandwidth
- Constant delay (unless using statistical multiplexing)
- Most used for phone calls

Cons:

- Wasted bandwidth if some channel doesn't use it's full bandwidth
- Difficult to add extra channels
- Not fit for interactive work (e.g. downloading, browsing)
  - This would require each browsing person to have a channel dedicated to them. When the user is not actually loading a page (e.g. just reading an article) the channel is 'inactive', however this bandwidth can't be used by other users.

### Packet switching

- Data is separated in multiple packets
- Each packet is individually routed through the network
  - This network is made up of multiple routers
- Store-and-forward
  - Each packet is only sent to the next router when the current router has received all the data in the packet.
  - This also means that each router has a queue for its packets.
  - While this queue is full the router discards any new packets it receives.

![](https://i.imgur.com/HMG37Cq.png)

## Communicatiemedia

### Types

Copper wires:

- Uses electrical singals
- Speed = 200.000 km/s
  - Yes this is actually about as fast as fiber. Fiber is still faster over longer distances because there is less interference, and there is "less need for processing and repeating of the signals."
- UTP (Unshielded Twisted Pair): twisted wires
- STP (Shielded Twisted Pair): twisted wires with a shield to protect against interference
- Twisting the wires reduces interference from the other wires.

Coax:

- Used for TV
- Broadband = multiple channels (FDM), requires modulation
- Baseband = no modulation aka 'raw' bits are pushed onto the wire

Fiber/glasvezel:

- Uses light
- Hardly any interference
- Speed = 200.000 km/s

### Modulation

- Modulation is the process of converting data into electrical signals optimized for transmission.
- Demodulation is the inverse (electrical -> data).
- Modem = modulator-demodulator = device that modulates and demodulates.

![](https://i.imgur.com/0xsSoCP.png)

### ADSL

- Uses FDM.
- POTS = Plain Old telephone System
- PSTN = Public Switched Telephone Network)
- Different bands for up- and downstream
  - Within these bands statistical multiplexing is used

![](https://i.imgur.com/xZ5llLQ.png)

## Network delays & co.

Sending data takes time:

- pushing the bits over the write
- propagation of the electrical signals
- processing delay
- queueing delay

### Transmission delay

Time that is required to send all the bits.

L = amount of bits  
R = transmission speed in bits/sec  
TransDelay = packet length / link bandwidth = L / R

```py
l = 1000
r = 1e6 # 1Mbps
t = l/r
t == 0.001 # seconds, or 1 millisecond
```

### Propagation delay

How long it takes a signal to travel over a wire.

Light speed = 300 000 km/s  
Fiber and copper wire = 200 000 km/s

m = distance (usually meters)
s = speed (usually meters per second)
PropDelay = length of link / speed over link = m / s

#### How long does it take to send 1 bit over 4000 km?

```py
# *1000 is used to convert from kilometers to meters
m = 4000 * 1000 # 4000 KM
s = 200 000 * 1000 # 200 000 KM/s
t = m / s
t == 0.02 # seconds, or 20 milliseconds
```

#### The width of a bit

Assuming that our speed is 10MBps, how 'long' is a bit on the wire?
Aka, how far did the first bit travel when we start sending the second bit?

```py
hz = 1/10_000_000 # 10 Mbps, aka one bit every 'hz' seconds.
dist = hz * 1e8 = 10 # meters
# TODO: Why multiply with 1e8?
```

#### Bandwidth-delay product

Bandwidth delay product is a measurement of how many bits can fill up a network link. It gives the maximum amount of data that can be transmitted by the sender at a given time before waiting for acknowledgment. Thus it is the maximum amount of unacknowledged data.

TODO: Math

### Queueing delay

Happens when you want to send multiple packets at the same time. The second packet has to wait for the first packet to be sent before it can start being transmitted.

TODO: Math stuff (see NW_slides08.pdf slide 52)

### Processing delay

E.g. processing time inside the router.

### RTT - Round Trip Time

Usually you want to know how long it takes to send a message, and how long it takes to receive a message.
When you add these two together you get the RTT (Round Trip Time), aka `RTT = delay_in_one_direction * 2`.

## Sources

- University of Utrecht INFONW Slides
- Wikipedia
- https://www.rfwireless-world.com/Terminology/FDM-versus-TDM.html
- www.fiber-optic-tutorial.com
- www.tutorialspoint.com
- inst.eecs.berkeley.edu
