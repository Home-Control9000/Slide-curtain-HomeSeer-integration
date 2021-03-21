# Slide-curtain-HomeSeer-integration

I wanted to integrate the Slide smart WIFI curtains from this Dutch company: https://nl.slide.store/ in my HomeSeer HomeAutomation system. 
The advantages is that you can install it very easy on your existing curtainsliders. The instructions are clear and easy.  

The first step is to activate the Slide with the Android/iOS APP. **Follow all instructions and setup/test the Slide before using the local control.** 
Then continue:

The APP is working with a Cloud connection but local control is more reliable and faster because communication between HomeSeer and Slide is directly without Internet cloudservices.
I integrated this in my HS4 HomeSeer system but it will also run on HS3 systems and with some adjustments on other HomeAutomation systems. 
HomeSeer is working with plugins but there is no one for Slide. The solution is to work with a virtual device which is triggering a Curl Event. 

Procedure:
The guys from Slide build a local API. 
You can activate it by sending a 'joining the Slide Beta Program' request to support@slide.store
The local API is activated and you will receive a 'Getting started document and some Postman JSON examples. 

I dont share this because they dont want this. So wait for your documents.
'We kindly request that you do not share these files with other people until we are fully ready to publish the local API documentation online. :-)'

Note:
IF YOU ACTIVATE THE LOCAL API THEN THE SLIDE APP DOESN'T WORK ANYMORE. This will be solved in the future the company says.
If you want, you can switch very easy to local and back to cloudcontrol (APP) if needed. I dont use the Slide APP anymore because control is always done with my HomeSeer system. 

The actually control is done with a curl script. So this solution you can use also in other Homeautomation systems. You can run HomeSeer on Windows and Linux. Im running Ubuntu (Linux) buth the curl command is also avaialble for Windows. Please read the HomeSeer manual for this.

**This will OPEN the curtains:**
curl --location --request POST '<IP-adress>/rpc/Slide.SetPos' \ --digest --user 'user:xxxxxxx' \ --header 'Content-Type: application/json' \ --header 'Content-Type: text/plain' \ --data-raw '{ "pos": 0 }'

**This will CLOSE the curtains:**
curl --location --request POST '<IP-adress>/rpc/Slide.SetPos' \ --digest --user 'user:xxxxxxx' \ --header 'Content-Type: application/json' \ --header 'Content-Type: text/plain' \ --data-raw '{ "pos": 1 }'

**This will HALF CLOSE the curtains: Adjust the "pos" value for other percentage**
curl --location --request POST '<IP-adress>/rpc/Slide.SetPos' \ --digest --user 'user:xxxxxxx' \ --header 'Content-Type: application/json' \ --header 'Content-Type: text/plain' \ --data-raw '{ "pos": 0.5 }'

HomeSeer Example for Curtain CLOSE/OPEN:

Notes:
-	Fill in your own Device Code by ‘user:’
-	Im using ‘slide’ as hostname. You can also directly use the IP adress from your Slide. Use DHCP reservation in your router so the IP adress is never changed. Read the manual from your router howto.
- In the HomeSeer example only OPEN and CLOSE is done. You can open partially by { "pos": 0.5 } (50%) or the value you want. Then you have to add dome more HomeSeer devices. 


