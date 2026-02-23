# RPi WiFi Provisioning
Python 3 script to help Raspberry Pi Zero W/ 2W join a WiFi network.

# Install and Run
Install using `crontab -e` on the command line. Add the following line at the end of the file, save and reboot.

<pre><code>@reboot sleep 10 && sudo python <i>[path to script]</i>/src/http_server.py -u </i>[path to script]</i>/ui $*</code></pre>

Run the following command to test the script:

<pre><code>sudo python <i>[path to script]</i>/src/http_server.py</code></pre>

# How it works

NetworkManager should be the active network manager on the device's host OS.

### 1. No valid WiFi network

At boot, a valid WiFi network is not found

### 2. Advertise Access Point

WiFi Connect detects available WiFi networks and opens an access point with a captive portal. Connecting to this access point with a mobile phone or laptop allows new WiFi credentials to be configured.

### 3. User Connects to Device Access Point

Connect to the opened access point on the device from your mobile phone or laptop. The access point SSID is, by default, `Rpi-hostname` where hostname if the device name. 

### 4. Portal is shown to User in Web Browser

After connecting to the access point from a mobile phone, it will detect the captive portal and open its web page. Opening any web page will redirect to the captive portal as well.  The default IP address is 192.168.42.1

### 5. User Enters Local WiFi Network Credentials in Portal

The captive portal provides the option to select a WiFi SSID from a list with detected WiFi networks and enter a passphrase for the desired network.

### 6. Device Connects to Local WiFi Network

When the network credentials have been entered, WiFi Connect will disable the access point and try to connect to the network. If the connection fails, it will enable the access point for another attempt. If it succeeds, the configuration will be saved by NetworkManager.

