1. a. 0-6 and 23-26
   b. 6-16 and 17-22
   c. triple duplicate ACK
   d. timeout
   e. 32
   f. 24
   g. 14 (or 15?)
   h. 7th round
   i. cwnd = 4, sshtresh = 4
   j. sshtresh = 21 or 24 (cwnd/2), cwnd = 1
   k. 2^(22-17)-1 = 31 packets

2. Because of TCP flow control the sender will not send data faster than the receiver can read and process the data.

3. 192 - ? = if 0 with 62 addresses (64 - 2 because of .255 and .0 address)
   160 - ? = if 1 with 30 addresses
   128 - ? = if 2 with 30 addresses
   rest = if 3

4.

if 0 = 224.0.0.0 - 224.0.255.255
if 1 = 224.1.0.0 - 224.1.255.255
if 2 = 224.2.0.0 - 225.255.255.255

a. ...

b.
11111000 10010001 01010001 01010101 -> if 3
11100000 00000000 11000011 00111100 -> if 0
11100001 10000000 00010001 01110111 -> if 2

5.

Prefix = 223.1.17/24
Subnet 1 = 60 ifs
Subnet 2 = 90 ifs
Subnet 3 = 12 ifs

Subnet 1 = 223.1.17.?/26
Subnet 2 = 223.1.17.?/25
Subnet 3 = 223.1.17.?/28

What about overlapping nets?

6. a. 128.119.40.129

7. on a nat you are only able to create outgoing connections, and not accept incoming connections. If everyone on the network can only create outgoing connections then there is no one to connect to.

8. 
