# USBModem Project
This project is an simple script to use an 3G USB Modem with a RaspberryPi

### Packages
The folowing packages are needed:
- minicom --> testing the modem
- ppp
- wvdial --> controling the 3G connection

### How to use the scripts
1. clone the git project:
```
  pi$ git clone git://github.com/jalcoriza/USBModem.git
```
2. Install the packets needed:
```
  pi$ sudo apt-get update
  pi$ sudo apt-get install minicom ppp wvdial
```
3. Save the original wvdial config file
```
   pi$ sudo mv /etc/wvdial.conf /etc/wvdial.conf_orginal
```
4. Copy the script needed (for example movistar)
```
   pi$ sudo cp wvdial.movistar.conf /etc/
   pi$ sudo chown root:dialout /etc/wvdial.movistar.conf
```
5. Create a soft link
```
  pi$ cd /etc
  pi$ sudo ln -s wvdial.freedompop.conf wvdial.conf
```
6. If your SIM has a PIN code xyzw, introduce it
```
  pi$ sudo minicom -D /dev/ttyUSB0
  at
  at+CPIN=xyzw
  CTRL-A x
```
7. Connect to the internet!!!
```
  pi$ sudo wvdial
```
8. Route the trafic through ppp0
```
  pi$ route -n
  pi$ route del default gw 192.168.1.1 eth0
  pi$ route add default gw 10.207.21.11 ppp0
```

