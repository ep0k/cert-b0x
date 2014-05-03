cert-b0x
==============

Database of private SSL/SSH keys for embedded devices


Dependencies
============

cert-b0x requires the OpenSSL, libpcap, and sqlite3 libraries:

    $ sudo apt-get install libssl-dev libpcap-dev libsqlite3-dev


Installation
============

cert-b0x can be built and installed using the typical configure/make process:

    $ ./configure
    $ make
    $ sudo make install


Usage
=====

Check a remote host for a known SSL key pair:

    $ cert-b0x --host=192.168.1.1
    $ cert-b0x --host=192.168.1.1:443

Check a pcap file for SSL certificate exchanges that match a known SSL private key:

    $ cert-b0x --pcap=file.pcap

Listen on a live network interface for SSL certificate exchanges that match a known SSL private key:

    # cert-b0x --interface=eth0

Check a local SSL certificate to see if it matches any that have a known SSL private key:

    $ cert-b0x --pem=cert.pem

Search the database for a given hardware/firmware version:

    $ cert-b0x --search=hardware.vendor=linksys
    $ cert-b0x --search=firmware.vendor=dd-wrt

List of all valid table/column values for use with the --search option (requires sqlite3):

    $ sqlite3 lbb.db
    sqlite> .schema
    CREATE TABLE certificates(id INTEGER PRIMARY KEY, fingerprint TEXT, certificate TEXT, key TEXT, description TEXT);
    CREATE TABLE firmware(id INTEGER PRIMARY KEY, device_id INTEGER, certificate_id INTEGER, vendor TEXT, description TEXT);
    CREATE TABLE hardware(id INTEGER PRIMARY KEY, vendor TEXT, model TEXT, revision TEXT, description TEXT);

