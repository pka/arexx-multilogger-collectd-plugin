Arexx Data Logger Protocol
==========================

(c) 2011-2012 Martin Mares <mj@ucw.cz>

All packets have fixed size of 64 bytes. The first byte is a packet
type, followed by type-dependent data.

Timestamps are 32-bit integers representing the number of seconds
since 2000-01-01 00:00:00 UTC.

Request packets  (from the PC to the logger)
--------------------------------------------

 * type 03:		Request sensor data

	The data part is probably unused.

 * type 04:		Set clock

	Data:	u32le	timestamp


Reply packets  (from the logger to the PC)
------------------------------------------

 * type 00:		Report sensor data

	The data part is a sequence of tuples, each tuple
	starts with its length.

		9-byte tuples:
			u8	tuple length (0x09)
			u16le	sensor ID
			u16be!	raw value
			u32le	timestamp

		10-byte tuples contain one extra byte:
			u8	signal quality (units unknown)

		A 0-byte tuple serves as a terminator.
