# CPU Communications

## Serial Bus

### Serial vs parallel communication


| Communication type | how it work | advantages | disadvantages |
| --- | --- | --- | --- |
| Serial | one bit at a time, sequentially | data integrity, high clock rate | single point of failure |
| Parallel | multiple bit at a time, asynchronously | could be faster | cost of cable and synchronization difficulties |

### Serial Buses

__NOTE__: One confusing aspect about serial interface is that many of them has more than one pins. For example, RS-232 has 7 pins. Actually only two of the 7 pins are actively to transmit data: one for receiving and one for transmitting. USB has 4 pins and two of them are for power and ground.

RS-232

USB(Universal Serial Bus)

## DMA(Direct Memory Access)

Sometimes, communication between hardware devices don't necessarily need to go through CPU. For example, reading file from hard disk to memory don't require every bytes to go through CPU.

## IRQ(Interrupt Request Queue)