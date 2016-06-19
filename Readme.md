# amridm2openhab

## Description

Using an [inexpensive rtl-sdr dongle](https://www.amazon.com/s/ref=nb_sb_noss?field-keywords=RTL2832U), it's possible to listen for signals from ERT compatible smart meters using rtlamr. This script runs as a daemon, launches rtl_tcp and rtlamr, and parses the output from rtlamr. If this matches your meter, it will push the data into openhab using the REST API.

OpenHAB items, rules, and portion of my sitemap are included

## Requirements

OpenHAB - Tested version 1.8 on Ubuntu 14.04
http://www.openhab.org/

rtl-sdr installed
http://sdr.osmocom.org/trac/wiki/rtl-sdr

Set dongle serial number with rtl-eeprom
http://manpages.ubuntu.com/manpages/trusty/man1/rtl_eeprom.1.html

install Go programming language & set gopath
`sudo apt-get install golang`
https://golang.org/doc/code.html#GOPATH

install rtlamr https://github.com/bemasher/rtlamr
`go get github.com/bemasher/rtlamr`

install perl packages
`sudo apt-get install libwww-mechanize-perl libfile-pid-perl`

## Install
create log file and set permissions
`sudo touch /var/log/amridm2openhab.log`
`sudo chmod 644 /var/log/amridm2openhab.log`
`sudo chown root:adm /var/log/amridm2openhab.log`

copy perl script into /usr/sbin and set executable
`sudo cp amridm2openhab /usr/sbin/amridm2openhab`
`sudo chmod +x /usr/sbin/amridm2openhab`

copy initscript into init.d and set executable
`sudo cp initscript-amridm2openhab /etc/init.d/amridm2openhab`
`sudo chmod +x /etc/init.d/amridm2openhab`

set initscript to run on boot and start
`update-rc.d amridm2openhab defaults 99`
`sudo service amridm2openhab start`

Optional, watch log file to verify it has started
`tail -f /var/log/amridm2openhab.log`