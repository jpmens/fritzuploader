# FritzUploader

A command-line uploader for the telephone directory (phone book) of a Fritz!Box. This software has been tested on a

* FRITZ!Box Fon WLAN 7270
* FRITZ!Box Fon WLAN 7390

This program can do all sorts of bad things for you, so be warned.

# Usage

It begins with a simple CSV file which can easily be generated from, say, LDAP, or CouchDB, MySQL or whatever other database you have your contacts in. The input file is the CSV such as


	#Name;home;work;mobile;quickdial;main
	Jolie, Jane;+1-555-1234;+49 555 6302547;0171-1234567;3;home
	Jones, Catherine;somenumber@sipgate.de;994995;;64;home

Lines beginning with a hash (`#`) are ignored, as are blank lines. Use the `csv2xml` script included herein to translate that to the XML required by the Fritz!Box. The program creates (or clobbers) a file called `phonebook.xml`.

	$ ./csv2xml < phonebook.csv 

Before uploading your `phonebook.xml` to the Fritz!Box, you'll want to backup the current telephone book; do so within the Web interface of the Fritz!Box.

To upload the `phonebook.xml`, run

	$ ./fritzuploader password
	Success: phonebook uploaded

where _password_ is the password you use to log in to your Fritz!Box Web interface. (Note this password will be visible by tools such as `ps` and it will be in your shell history. If you're not alone on your machine, fix it by hardcoding it into the program.)

Beware: the phone book is written into flash memory on the Fritz!Box -- don't run this program too frequently.

# Bugs

Yeah, sure. 

If the upload fails, e.g. because the XML contains rubbish, we don't get an HTTP error code or such; instead, the Fritzbox returns an HTML page from which you'll have to determine what went wrong.
