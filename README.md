# Slide-curtain-HomeSeer-integration

I wanted to integrate the Slide smart WIFI curtains from this Dutch company: https://nl.slide.store/ in my HomeSeer HomeAutomation setup. 
The advantages from Slide is that you can install it very easy on your existing curtainsliders. I found the instructions very clear and easy. 

HomeSeer is working with plugins for third party products but unfortunately there is no Slide plugin. 
The solution is to work with a virtual device which is triggering a Curl Event. 

The first step is to install and then activate the Slide with the Android/iOS APP. **Follow all instructions and setup/test the Slide before using the local control.** 
Then continue:

The APP is working with a Cloud connection but local control is more reliable and faster because communication between HomeSeer and Slide is directly without Internet cloudservices.
I integrated this in my HS4 HomeSeer system but it will also run on HS3 systems and with some adjustments on other HomeAutomation systems. 

Procedure:
The guys from Slide build a local API which is great :) 
You can activate it by sending a 'joining the Slide Beta Program' request to support@slide.store
They will reply and the local API is activated and you will receive a 'Getting started document and some Postman JSON examples' 

I dont share this documentation because they dont want this. So wait for your own documents.
'We kindly request that you do not share these files with other people until we are fully ready to publish the local API documentation online. :-)'

Note:
**IF YOU ACTIVATE THE LOCAL API THEN THE SLIDE APP DOESN'T WORK ANYMORE.** This will be solved in the future the company says.
If you want, you can switch very easy to local and cloudcontrol (APP) if needed.
I don't use the Slide APP anymore. Slide Control is always done with my HomeSeer system (Alexa, Google Home, Events etc) 

The actually control is done with a simple curl script. This you can use also in other HomeAutomation systems. You can run HomeSeer on Windows and Linux. Im running Ubuntu (Linux) buth the curl command is also avaialble for Windows. Please read the HomeSeer manual for this.

**This will OPEN the curtains:**
curl --location --request POST 'IP/rpc/Slide.SetPos' \ --digest --user 'user:xxxxxxx' \ --header 'Content-Type: application/json' \ --header 'Content-Type: text/plain' \ --data-raw '{ "pos": 0 }'

**This will CLOSE the curtains:**
curl --location --request POST 'IP/rpc/Slide.SetPos' \ --digest --user 'user:xxxxxxx' \ --header 'Content-Type: application/json' \ --header 'Content-Type: text/plain' \ --data-raw '{ "pos": 1 }'

**This will HALF CLOSE the curtains: Adjust the "pos" value for other percentage**
curl --location --request POST 'IP/rpc/Slide.SetPos' \ --digest --user 'user:xxxxxxx' \ --header 'Content-Type: application/json' \ --header 'Content-Type: text/plain' \ --data-raw '{ "pos": 0.5 }'

HomeSeer Example for Curtain CLOSE/OPEN:
[HomeSeer example](./HomeSeer-Slide-Integration-Example.pdf)

Notes:
-	Fill in your own Device Code by ‘user:’
-	Im using ‘slide’ as hostname. Its added in /etc/hosts. You can also directly use the IP adress from your Slide. Use DHCP reservation in your router so the IP adress is never changed. Read the manual from your router howto.
- In the HomeSeer example only OPEN and CLOSE is done. For me this is enough. You can open partially by { "pos": 0.5 } (50%) or the value you want. Then you have to add some more Virtual devices. For example Slide 30%, Slide 80% etc.


