# Libfins API Reference

Libfins is a library to communicate over the FINS/TCP protocol over ethernet with Omron PLCs. The library is written
in C and can be compiled with any modern C compiler. The API to the library is described in this document.

*This document is currently work in progress.*

## Constants

| Name | Description |
| :--- | :--- |
|**`FINS_CPU_MODE_MONITOR`**|Status code indicating that the PLC CPU is in monitor mode|
|**`FINS_CPU_MODE_PROGRAM`**|Status code indicating that the PLC CPU is in program mode|
|**`FINS_CPU_MODE_RUN`**|Status code indicating that the PLC CPU is in run mode|

|Name|Description|
|:---|:---|
|**`FINS_DEFAULT_PORT`**|The default port number used by the FINS/TCP protocol|

|Name|Description|
|:---|:---|
|**`FINS_FORCE_RELEASE_TO_OFF`**|The bit force must be released and the bit value is reset|
|**`FINS_FORCE_RELEASE_TO_ON`**|The bit force must be released and the bit value is set|
|**`FINS_FORCE_RELEASE`**|The bit force must be released and the bit value is unchanged|
|**`FINS_FORCE_RESET`**|The bit status must be forced and the bit value is reset|
|**`FINS_FORCE_SET`**|The bit status must be forced and the bit value is set|

|Name|Description|
|:---|:---|
|**`FINS_MSG_0`**|Bit mask indicating user program generated message MSG 0|
|**`FINS_MSG_1`**|Bit mask indicating user program generated message MSG 1|
|**`FINS_MSG_2`**|Bit mask indicating user program generated message MSG 2|
|**`FINS_MSG_3`**|Bit mask indicating user program generated message MSG 3|
|**`FINS_MSG_4`**|Bit mask indicating user program generated message MSG 4|
|**`FINS_MSG_5`**|Bit mask indicating user program generated message MSG 5|
|**`FINS_MSG_6`**|Bit mask indicating user program generated message MSG 6|
|**`FINS_MSG_7`**|Bit mask indicating user program generated message MSG 7|
|**`FINS_MSG_ALL`**|Bit mask indicating all user program generated messages|

|Name|Description|
|:---|:---|
|**`FINS_MULTI_TYPE_BIT`**|The data must be returned as a bit value|
|**`FINS_MULTI_TYPE_BIT_FORCED`**|The data must be returned as a bit with forced status|
|**`FINS_MULTI_TYPE_DOUBLE`**|The data must be returned as a 64 bit floating point number|
|**`FINS_MULTI_TYPE_FLOAT`**|The data must be returned as a 32 bit floating point number|
|**`FINS_MULTI_TYPE_INT16`**|The data must be returned as a signed 16 bit integer|
|**`FINS_MULTI_TYPE_INT32`**|The data must be returned as a signed 32 bit integer|
|**`FINS_MULTI_TYPE_SBCD16`**|The data must be returned as a signed 16 bit BCD value|
|**`FINS_MULTI_TYPE_SBCD32`**|The data must be returned as a signed 32 bit BCD value|
|**`FINS_MULTI_TYPE_UBCD16`**|The data must be returned as an unsigned 16 bit BCD value|
|**`FINS_MULTI_TYPE_UBCD32`**|The data must be returned as an unsigned 32 bit BCD value|
|**`FINS_MULTI_TYPE_UINT16`**|The data must be returned as an unsigned 16 bit integer|
|**`FINS_MULTI_TYPE_UINT32`**|The data must be returned as an unsigned 32 bit integer|
|**`FINS_MULTI_TYPE_WORD`**|The data must be returned as a 16 bit wordt with forced status|

|Name|Description|
|:---|:---|
|**`FINS_RETVAL_SUCCESS`**|The function executed successfully|
|**`FINS_RETVAL_SUCCESS_LAST_DATA`**|The function executed successfully and the last available data is returned|
|**`FINS_RETVAL_CANCELED`**|The execution of the function was cancelled|
|**`FINS_RETVAL_ABORTED`**|The execution of the function was aborted|
|**`FINS_RETVAL_MAX_ERROR_COUNT`**|The maximum allowed error count was reached and the connection is closed|
|**`FINS_RETVAL_SYNC_ERROR`**|A synchronization error occured|
|**`FINS_RETVAL_CLOSED_BY_REMOTE`**|The connection was closed by the remote peer|
|**`FINS_RETVAL_NO_FINS_HEADER`**|The request or response packet had an invalid FINS header|
|**`FINS_RETVAL_DATA_LENGTH_TOO_LONG`**|The length of the packet is too long|
|**`FINS_RETVAL_COMMAND_NOT_SUPPORTED`**|The issued FINS command is not supported by the remote CPU|
|**`FINS_RETVAL_ALL_CONNECTIONS_IN_USE`**|All the connections are in use|
|**`FINS_RETVAL_NODE_ALREADY_CONNECTED`**|The node is already connected|
|**`FINS_RETVAL_NODE_IP_PROTECTED`**|The IP address of the node is connected|
|**`FINS_RETVAL_CLIENT_NODE_OUT_OF_RANGE`**|The client node number is out of range|
|**`FINS_RETVAL_SAME_NODE_ADDRESS`**|The client and server use the same node address|
|**`FINS_RETVAL_NO_NODE_ADDRESS_AVAILABLE`**|All free node address slots are in use|
|**`FINS_RETVAL_TRY_LATER`**|The system is busy, please try again later|
|**`FINS_RETVAL_NOT_INITIALIZED`**|The FINS contect is not initialized|
|**`FINS_RETVAL_NOT_CONNECTED`**|There is no active connection with the remote peer|
|**`FINS_RETVAL_OUT_OF_MEMORY`**|An out of memory error occured|
|**`FINS_RETVAL_INVALID_IP_ADDRESS`**|An invalid IP address was specified|
|**`FINS_RETVAL_NO_READ_ADDRESS`**|No remote read address specified in function call|
|**`FINS_RETVAL_NO_WRITE_ADDRESS`**|No remote write address specified in function call|
|**`FINS_RETVAL_NO_DATA_BLOCK`**|There was no data block specified in the function call to store received or to send data|

## Structures

### `struct fins_cpustatus_tp;`

#### Fields

| Field | Type | Description |
| :--- | :--- | :--- |
|**`message_exists`**|`bool[8]`|An array of bits indicating if a user generated message is available|
|**`running`**|`bool`|**`true`** if the CPU is currently running|
|**`flash_writing`**|`bool`|**`true`** if the PLC is currently busy writing to flash memory|
|**`battery_present`**|`bool`|**`true`** if a memory backup battery is present in the PLC|
|**`standby`**|`bool`|**`true`** if the CPU is currently in standby mode|
|**`fatal_memory_error`**|`bool`|**`true`** if a fatal memory error in the PLC occured|
|**`fata_io_bus_error`**|`bool`|**`true`** if a fatal I/O bus error occured|
|**`fata_duplication_error`**|`bool`|**`true`** if a fatal duplication error occured|
|**`fatal_inner_board_error`**|`bool`|**`true`** if a fatal inner board error occured|
|**`fatal_io_point_overflow`**|`bool`|**`true`** if a fatal I/O point overflow occured|
|**`fatal_io_setting_error`**|`bool`|**`true`** if a fatal I/O setting error occured|
|**`fatal_program_error`**|`bool`|**`true`** if a fatal program error occured|
|**`fatal_cycle_time_error`**|`bool`|**`true`** if the PLC stopped due to a cycle time overflow|
|**`fatal_fals_error`**|`bool`|**`true`** if the PLC stopped due to a user program generated FALS error|
|**`fal_error`**|`bool`|**`true`** if the user program generated a non-fatal FAL error|
|**`duplex_error`**|`bool`|**`true`** if a non-fatal duplex error occured|
|**`interrupt_task_error`**|`bool`|**`true`** if a non-fatal interrupt task error occured|
|**`basic_io_unit_error`**|`bool`|**`true`** if a non-fatal basic I/O unit error occured|
|**`plc_setup_error`**|`bool`|**`true`** if a non-fatal PLC setup error occured|
|**`io_verification_error`**|`bool`|**`true`** if a non-fatal I/O verification error occured|
|**`inner_board_error`**|`bool`|**`true`** if a non-fatal inner board error occured|
|**`cpu_bus_unit_error`**|`bool`|**`true`** if a non-fatal CPU bus unit error occured|
|**`special_io_unit_error`**|`bool`|**`true`** if a non-fatal special I/O unit error occured|
|**`sysmac_bus_error`**|`bool`|**`true`** if a non-fatal sysmac bus error occured|
|**`battery_error`**|`bool`|**`true`** if a non-fatal battery error occured|
|**`cs1_cpu_bus_unit_setting_error`**|`bool`|**`true`** if a non-fatal error occured in the settings of a CS1 CPU bus unit|
|**`special_io_unit_setting_error`**|`bool`|**`true`** if q non-fatal error occured in the settings of a special I/O unit|
|**`run_mode`**|`uint8_t`|The current operating mode of the CPU|
|**`error_code`**|`uint16_t`|The active error code with the highest priority|
|**`error_message`**|`char[17]`|The current active error message in ASCII text|

#### Description

The structure `fins_cpustatus_tp` is used to store the actual status of the CPU of a PLC when the function
`finslib_cpu_unit_status_read()` is called.

### `struct fins_cycletime_tp;`

#### Fields

| Field | Type | Description |
| :--- | :--- | :--- |
|**`min`**|`uint32_t`|The minimum cycle time of the PLC since the last cycle time reset. The time is expressed in units of 0.1 msec.|
|**`avg`**|`uint32_t`|The average cycle time over the last eight cycles of the PLC. The time is expressed in units of 0.1 msec.|
|**`max`**|`uint32_t`|The maximum cycle time of the PLC since the last cycle time reset. The time is expressed in uints of 0.1 msec.|

#### Description

The structure `fins_cycletime_tp` is used by the function `finslib_cycle_time_read()` to store the minimum, average and maximum
cycle times of the PLC.

### `struct fins_unitdata_tp;`

#### Fields

| Field | Type | Description |
| :--- | :--- | :--- |
|**`model`**|`char[21]`|The model name of the unit|
|**`unit`**|`uint8_t`|The unit number of the unit|

#### Description

The structure `fins_unitdata_tp` is used to store the information of one special I/O unit in a PLC system when unit data
is requested with a call to the `finslib_connection_data_read()` function.

## Functions

### `finslib_memory_area_read_word( sys, start, data, num_words );`

#### Parameters

| Parameter | Type | Description |
| :--- | :--- | :--- |
|**`sys`**|`struct fins_sys_tp *`|A pointer to a structure with the FINS context|
|**`start`**|`const char *`|An ASCII string describing the first memory element to retrieve|
|**`data`**|`unsigned char *`|Pointer to the buffer where the result must be stored|
|**`num_words`**|`size_t`|The number of words to return|

#### Returns

| Type | Description |
| :--- | :--- |
|`int`|A return value from the list `FINS_RETVAL_...` indicating the result of the query|


The function `finslib_memory_area_read_word()` can be used to retrieve a block of 16 bit words from a memory
are in a remote PLC. The connection with the PLC should already be present before this function is called.

Data is transferred unmodified from the FINS data stream to the caller supplied buffer. As this function
returns a number of words, the size of the data buffer in bytes should be at least twice the number of words
requested. Enough dataspace is the responsibility of the calling function, but `finslib_memory_area_read_word()`
will return an error if a NULL pointer is provided for data storage.

The start of the memory area is provided as an ASCII string which represents the starting address in human
readable format. Example formats are **`CIO20`** and **`W100`**.

The requested number of words is not limited by the amount of data a PLC can send in one FINS packet because
`finslib_memory_area_read_word()` will automatically use multiple request at the FINS layer if the dataset will
be too large.

The return value is either **`FINS_RETVAL_SUCCESS`** when the function succeeded, or one of the other
**`FINS_RETVAL_`** values if an eror occurs. In the latter case the data in the return buffer is unreliable and
should not be used.