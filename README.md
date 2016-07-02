# PCAPNG File Parser #

[![Build Status](https://travis-ci.org/akinaru/pcapng-decoder.svg?branch=master)](https://travis-ci.org/akinaru/pcapng-decoder)
[ ![Download](https://api.bintray.com/packages/akinaru/maven/pcapng-parser/images/download.svg) ](https://bintray.com/akinaru/maven/pcapng-parser/_latestVersion)
[![Codacy Badge](https://api.codacy.com/project/badge/Grade/1188df87489749a48978a5d953662d18)](https://www.codacy.com/app/bmartel.fr/pcapng-decoder?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=akinaru/pcapng-decoder&amp;utm_campaign=Badge_Grade)
[![Javadoc](http://javadoc-badge.appspot.com/com.github.akinaru/pcapng-parser.svg?label=javadoc)](http://javadoc-badge.appspot.com/com.github.akinaru/pcapng-parser)
[![License](http://img.shields.io/:license-mit-blue.svg)](LICENSE.md)

decode pcapng file with following sections  :
* Section Header
* Interface Description
* Interface Statistics
* Enhanced Packet
* Name Resolution

## Include in your project

* from gradle 

```
compile 'com.github.akinaru:pcapng-parser:1.2'
```

* from release archive

https://github.com/akinaru/pcapng-decoder/releases

## Run example

```
./gradlew run -PappArgs="['-f', 'path_to_file/pcapfile/exemple.pcapng'  , '-v' ]"

```

|  args            | description                                        |
|------------------|----------------------------------------------------|
| -f <file.pcapng> | input file                                         |
| -v               | verbose, will show all section parsing content     |

## How to user ?

```
byte[] dataFromFile = readFile("test.pcapng");

PcapDecoder pcapNgDecoder = new PcapDecoder(dataFromFile);
pcapNgDecoder.decode();
```

You will access all parsed data from pcapNgDecoder object.
A complete example is present in ``DisplayAllPacket`` class

getSectionList() : retrieve all sections Object

Access to section type is possible with reflection using instanceof with a set of interface defined in package ``fr.bmartel.pcapdecoder.structure.types.inter`` :

4 sections are available :

* `ISectionHeaderBlock`
* `IEnhancedPacketBlock`
* `IStatisticsBLock`
* `IDescritpionBlock`
* `INameResolutionBlock`

A ``getSectionList().get(index) instanceof ISectionHeaderBlock`` will permit you to cast the latter interface to get access to the section's characteristics.

packet data in Enhanced Packet Block is left in packet source endianness (make it easier to compare with Wireshark result)

## Example output

```
##########################################################<br/>
SECTION HEADER BLOCK<br/>
Major version      : 0<br/>
Minor version      : 1<br/>
OS                 : Linux 3.8.0-19-generic<br/>
user application   : Dumpcap 1.10.2 (SVN Rev 51934 from /trunk-1.10)<br/>
##########################################################<br/>
SECTION INTERFACE DESCRIPTION BLOCK<br/>
Link type             : LINKTYPE_IEEE802_11_RADIO<br/>
Snap len              : 65535<br/>
interface name        : wlan0<br/>
timestamp resolution  : 6<br/>
interface OS name     : Linux 3.8.0-19-generic<br/>
##########################################################<br/>
SECTION ENHANCED PACKET BLOCK<br/>
interface id             : 0<br/>
timestamp in millis      : Sat Apr 18 12:13:41 CEST 2015<br/>
captured length          : 185<br/>
packet length            : 185<br/>
packet data              : 00 | 00 | 12 | 00 | 2E | 48 | 00 | 00 | 10 | 02 | A3 | 09 | A0 | 00 | C2 | 07 | 00 | 00 | 80 | 00 | 00 | 00 | FF | FF | FF | FF | FF | FF | 00 | 24 | D4 | 6B | 0C | 5D | 00 | 24 | D4 | 6B | 0C | 5D | 00 | E5 | 60 | 01 | 25 | DE | 32 | 03 | 00 | 00 | 60 | 00 | 01 | 04 | 00 | 08 | 46 | 72 | 65 | 65 | 57 | 69 | 66 | 69 | 01 | 08 | 82 | 84 | 8B | 96 | 2C | 0C | 12 | 18 | 03 | 01 | 0C | 05 | 04 | 00 | 02 | 00 | 00 | 2A | 01 | 04 | 32 | 05 | 24 | 30 | 48 | 60 | 6C | 2D | 1A | 6C | 00 | 03 | FF | FF | FF | 00 | 01 | 00 | 00 | 00 | 00 | 00 | 00 | 00 | 01 | 00 | 00 | 00 | 00 | 00 | 00 | 00 | 00 | 00 | 00 | 3D | 16 | 0C | 00 | 13 | 00 | 00 | 00 | 00 | 00 | 00 | 00 | 00 | 00 | 00 | 00 | 00 | 00 | 00 | 00 | 00 | 00 | 00 | 00 | 7F | 08 | 00 | 00 | 00 | 00 | 00 | 00 | 00 | 40 | DD | 18 | 00 | 50 | F2 | 02 | 01 | 01 | 00 | 00 | 03 | A4 | 00 | 00 | 27 | A4 | 00 | 00 | 42 | 43 | 5E | 00 | 62 | 32 | 2F | 00 | A3 | 26 | 13 | 07<br/>
##########################################################<br/>
SECTION INTERFACE STATISTICS BLOCK<br/>
interface id             : 0<br/>
timestamp in millis      : Sat Apr 18 12:16:43 CEST 2015<br/>
capture start time       : Sat Apr 18 12:13:41 CEST 2015<br/>
capture end time         : Sat Apr 18 12:16:43 CEST 2015<br/>
packet received count    : 9493<br/>
packet drop count        : 0<br/>
##########################################################<br/>
```

## Compatibility

JRE 1.7 compliant

## Build

Gradle using IntelliJ IDEA or Eclipse

## Specifications 

https://www.winpcap.org/ntar/draft/PCAP-DumpFileFormat.html

## License

The MIT License (MIT) Copyright (c) 2015-2016 Bertrand Martel