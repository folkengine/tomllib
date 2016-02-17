* Everywhere
	- [ ] Switch back to using nom now that the new version has been released

* primitives.rs
	- [ ] Implement get_keychain_key
	- [ ] Implement get_full_key
	- [ ] Implement get_key_parent
	- [ ] Change Key::Str to just hold an &'a str again
	- [ ] Fix DateTime to allow only Date, only DateTime (no fractional seconds), only DateTime (with fractional seconds), Full DateTime with offset
	- [ ] Change TimeOffset::Z to TimeOffset::Zulu?
	- [ ] Change '+'/'-' to enum

* ast/structs.rs
	- [ ] Re-implement HashValue to have a list of children or max index of children
	- [ ] Fix DateTime to allow only Date, only DateTime (no fractional seconds), only DateTime (with fractional seconds), Full DateTime with offset
	- [ ] Change TimeOffset::Z to TimeOffset::Zulu?
	- [ ] Change '+'/'-' to enum

* objects.rs
	- [ ] In array_table when adding to existing table get_key_parent and add the new index as a child in the map, then add full_key to the map with None value
	- [ ] In array_table and std_table if table keys imply subtables that don't exist, add the implied tables as std_tables to the map with None value and add add their subkeys as children
	- [ ] In array_table if get_key_parent exists and has no indexed children, then it is an error (see toml-test/invalid/table_array_implicit)
	- [ ] In array_table when encountering a new table that isn't a subtable of the last table, rebuild last_array_tables and last_array_tables_index by starting at the first subkey, looking up it's children and so-on, if the array_table already exists
	- [ ] In array_table and std_table always add new table to map with None value
	- [ ] In array_value insert_key_val_into_map

* parser.rs
	- [ ] Change Key::Str to just hold an &'a str again
	- [ ] Implement reconstruct_inline_table
	- [ ] Need to rehash keys values when reconstituting tables and arrays when their keys or structure has changed and also change their parent's children
		- [ ] Array is replaced with scalar => remove keys for replaced array values
		- [ ] Scalar is replaced with array => add new keys for new array values
		- [ ] Array is truncated => remove keys for values that were removed
		- [ ] Array is lengthened => add keys for new values that were added
		- [ ] Inline table is replaced with a scalar => remove keys for replaced inline table key/values
		- [ ] Scalar is replaced with inline table => add new keys for new inline table key/values
		- [ ] Inline table is truncated => remove keys for values that were removed
		- [ ] inline table is lengthened => add keys for new values that were added
		- [ ] Implement default formatting for lengthened arrays
		- [ ] Implement default formatting for lengthened inline-tables (TOML already suggests a default formatting)
	- [ ] Implement get_errors
	- [ ] Add unit tests for getting values
	- [ ] Add unit tests for setting values
	- [ ] Add unit tests to check the map to make sure removed keys are gone

* tests/assets.rs
	- [ ] Add failure/error tests for invalid toml-test's
	- [ ] Add toml/examples/example-v0.4.0.toml to success tests

* tests/parser_tests.rs
	- [ ] Add integration tests for parser, like unit tests, but load a larger document -> validate, do a bunch of gets -> validate, do a bunch of sets -> validate, then do a bunch of gets