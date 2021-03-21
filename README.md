# Slide-curtain-HomeSeer-integration

I bought a Slide smart WIFI curtain by this Dutch company: https://nl.slide.store/
You can control it with a APP on Android and IOS (iPhone) devices.
This is done with a Cloud connection which is working well but i needed local control from my homeautomation system because this is more reliable and faster.
I integrated this in my HS4 HomeSeer system but it will also run on HS3 systems. 

The guys from Slide build a local API. 
You can activate it by request joining the Slide Beta Program by sending a E-mail to support@slide.store
You will receive a 'Getting started document and some Postman JSON examples.



--
Slide Local API (Beta)

Getting started
The Slide Local API is, in it’s current form, intended as a first version, and expected to undergo significant expansions in later updates. The focus of the current API is to allow you to directly control the curtains, and we assume you handle all action logic (e.g. triggers) within your home automation tool of choice. 

Postman
Because this API is not yet published, I am attaching two documents that you can open in Postman (https://www.getpostman.com/), an easy-to-use multi-platform API Management tool. One file contains the collection (e.g. the API calls), the other the environment (which sets, among others, your Slide Device Code). 

We kindly request that you do not share these files with other people until we are fully ready to publish the local API documentation online. :-)

Enabling the Local API
Your Slides are compatible with the Local API, out of the box. By default, this HTTP API is disabled, because system restrictions prevent it from running concurrently with our Cloud API (more on that below).
In order to enable the local API, we use the reset button (hole) on the bottom of Slide. There are two holes on either side of the power plug hole, the reset button is indicated in the photo below. You will need a small pincer or similar to reach the button inside. 
Briefly press the reset button twice, with about 0.5 second between the two presses.
1.	If you see the LED (the other hole) rapidly flash five times, you have disabled the Cloud API and enabled the Local API.
2.	If you see the LED slowly flash two times, you have enabled the Cloud API and disabled the Local API.

Using the Local API
Now that Slide is in Local API mode, you can reach the device locally through HTTP with Digest Authentication.
Currently we do not yet support discovery (such as dns-sd, zeroconf etc.) so you will have to identify which local IP address (192.168.xxx.xxx) your Slide is using. Due to a known bug all Slides currently have the hostname “espressif" on the local network, which might make this exercise slightly annoying if you have many Slides online – apologies for that.
The next step is to edit the Environment in Postman with the Local IP Address and the Device Code (which is on top of Slide and the Welcome Sheet, as used during installation). The Device Code is required for Digest Authentication.
In case of multiple Slides, we recommend that you duplicate the environment so that you have 1 for each Slide in order to quickly toggle between them. The Local API commands in themselves only target one Slide at a time, since this is direct-to-device communication.
Features of the Local API:
-	Read Slide Device ID (MAC)
-	Re-calibrate Slide
-	Request current Position
-	Request whether Touch&Go is on or off (currently not yet adjustable)
-	Set curtain position (a float between 0 and 1)
-	(Immediate) stop of the motor during a movement (‘Hard abort’)
-	Change WiFi network credentials of Slide

Known limitations of current Local API spec:
1.	When the Local API is enabled, the Cloud API (and therefore, the Slide Mobile App) are not yet available. The Cloud and Local APIs use a different form of authentication. The Slide firmware currently does not handle both HTTP Digest Auth and MQTTS SSL Auth simultaneously. This is a work in progress, but in the meantime we decided to already offer the Local API for those that have a strong preference for non-cloud connectivity. 
2.	The Slide Device Name is not yet correctly displayed, which means you will have to bind the Slide device (in the home automation tool of your choice) to a human-readable name by yourself.

Planned features of the Local API
1.	The ability to read the Slide Device Name and Zone Name from within the Local API, and possibly adjust it from within the Local API as well.
2.	DNS-SD Support to allow device discovery on the local network.
3.	A unique hostname for each Slide, possibly using the user-defined Device Name prefixed by ‘Slide –‘
4.	The ability to enable/disable Touch&Go through the Local API
5.	Eventually running the Local API with the Cloud API. This may require running the Local API over MQTT as a protocol, which would mean it is not backward compatible with the current version. 
--







