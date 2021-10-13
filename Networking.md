# Networking Notes

## TODO

- Circuitswitching
- Packetswitching
- Layers (NOT the OSI layer, we only use 5 layers)

## Connection types

### Connection-oriented

### Connection-less

## Transport Protocols

### TCP

### UDP

### FDM & TDM (and both)

## Communicatiemedia

## Network delays & co.

### Transmission delay

Time that is required to send all the bits.

L = amount of bits  
R = transmission speed in bits/sec  
TransDelay = L / R  

```py
l = 1000
r = 1e6 # 1Mbps
t = l/r
t == 0.001 # seconds, or 1 millisecond
```

### Propagation delay

How long it takes a signal to travel over a wire.

Light speed = 300 000 km/s  
Fiber = 200 000 km/s  
 
m = distance (usually meters)  
s = speed (usually meters per second)  
PropDelay = m / s

```py
# *1000 is used to convert from kilometers to meters
m = 4000 * 1000 # 4000 KM
s = 200 000 * 1000 # 200 000 KM/s
t = m / s
t == 0.02 # seconds, or 20 milliseconds
```

### Queueing delay

Happens when you want to send multiple packets at the same time. The second packet has to wait for the first packet to be sent before it can start being transmitted.

TODO: Math stuff (see NW_slides08.pdf slide 52)

### Processing delay

E.g. processing time inside the router.

### RTT - Round Trip Time

Usually you want to know how long it takes to send a message, and how long it takes to receive a message.
When you add these two together you get the RTT (Round Trip Time), aka `RTT = delay_in_one_direction * 2`.
