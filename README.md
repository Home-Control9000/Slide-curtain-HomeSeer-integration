# Slide-curtain-HomeSeer-integration

I wanted to integrate the Slide smart WIFI curtains from this Dutch company: https://nl.slide.store/ in my HomeSeer homeautomation system. 
The advantages from these curtains that you can install it very easy on your existing curtainsliders. The instructions are clear and easy.  

You can control it with a APP on Android and IOS (iPhone) devices.
This is done with a Cloud connection which is actually working very well but i needed local control from my homeautomation system because this is more reliable and faster.
I integrated this in my HS4 HomeSeer system but it will also run on HS3 systems and with some adjustments on other HomeAutomation systems. 

The guys from Slide build a local API. 
You can activate it by sending a 'joining the Slide Beta Program' request to support@slide.store
The local API is activated and you will receive a 'Getting started document and some Postman JSON examples.
[Slide API documentation](Local_API_documentation.zip)

Note:
IF YOU ACTIVATE THE LOCAL API THEN THE SLIDE APP DOESN'T WORK ANYMORE. This will be solved in the future they say.
If you want you can switch very easy to local and back to cloudcontrol (APP) if needed. I dont use the Slide APP anymore because control is done with my HomeSeer system. 

The actually control is done with a curl script. So this solution you can use also in other Homeautomation systems.

This will OPEN the curtains:
curl --location --request POST 'slide/rpc/Slide.SetPos' \ --digest --user 'user:xxxxxxx' \ --header 'Content-Type: application/json' \ --header 'Content-Type: text/plain' \ --data-raw '{ "pos": 0 }'

This will complete CLOSE the curtains:
curl --location --request POST 'slide/rpc/Slide.SetPos' \ --digest --user 'user:xxxxxxx' \ --header 'Content-Type: application/json' \ --header 'Content-Type: text/plain' \ --data-raw '{ "pos": 0 }'

This will HALF CLOSE the curtains:
curl --location --request POST 'slide/rpc/Slide.SetPos' \ --digest --user 'user:xxxxxxx' \ --header 'Content-Type: application/json' \ --header 'Content-Type: text/plain' \ --data-raw '{ "pos": 0.5 }'

In HomeSeer i created a virtual device and some events to control it. Example: 

