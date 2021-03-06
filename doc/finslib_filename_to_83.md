# Libfins API Reference

### `finslib_filename_to_83( infile, outfile );`

### Parameters

| Parameter | Type | Description |
| :--- | :--- | :--- |
|**`infile`**|`const char *`|The filename in human readable format|
|**`outfile`**|`char *`|Location to store the to 8.3 format converted filename|

### Return Value

| Type | Description |
| :--- | :--- |
|`int`|A return value from the list [`FINS_RETVAL_...`](fins_retval.md) indicating the result of the query|

### Description

### See Also

* [`FINS_RETVAL...`](fins_retval.md) &ndash; Libfins function return code list
* [`finslib_file_name_read();`](finslib_file_name_read.md)
* [`finslib_file_read();`](finslib_file_read.md)
* [`finslib_file_write();`](finslib_file_write.md)
* [`finslib_valid_directory();`](finslib_valid_directory.md)
* [`finslib_valid_filename();`](finslib_valid_filename.md)
