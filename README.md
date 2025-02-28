# Updates from my conversation with Wyze

**_TLDR:_ Some functionality has to go away (motion sensors, contact sensors, and camera motion detection). We account for over 50% of their traffic while being a _very_ small minority of their userbase. I would like to request some help fixing a bug with the auth endpoint -> contact me here if you can help: [joshua@mulliken.net](mailto:joshua@mulliken.net)**

My conversation with the people at Wyze was very productive. We are planning a way forward to continue the integration with HA while being good citizens of their platform. 

Based on the information I have from this repo and the _limited_ information they were able to share, this integration is used by between 1,000-10,000 individual HA instances. This number is increasing steadily; however, it is still a tiny fraction of the multiple millions of people who use their services. Even though we are such a small percentage of their userbase, we account for over 50% of the traffic to their servers. This amounts to a tangible cost (monetarily for Wyze) and usability effect on the rest of their users.

## Issues that need to be resolved

### Point 1: Motion Sensors, Contact Sensors, and Camera Motion Detection

They want me to disable the binary sensor devices as these are absolutely pummeling their servers. I will release an update tonight that removes them _entirely_ until we can find another way to implement them. If we don't all upgrade to that version and stop requesting from their API for those devices, they have said they are considering shutting down **all** access from Home Assistant.

### Point 2: Requests to the Auth Endpoint

They have also informed me that we have a bug that is causing requests to their authorization endpoint way more than is necessary (1 for every request) which I will be investigating <- **and would appreciate any debugging assistance on this point from the community**

## Updates on Public APIs/Legit Home Assistant Integration

Some employees of Wyze use the integration 😄!! They definitely want it to keep working! I asked about APIs or methods that I could use to reduce the load on their servers while still maintaining all functionality, and they were unable to speak to their future roadmap. They offered me an NDA, but since I am speaking to you now, it should be obvious that I declined.

They have promised to share information on how to implement the 2FA in line with their requirements going forward and did say that they will be requiring 2FA for all logins at some point in the near future. I will be working with them to ensure that this is working in the integration before that requirement is in place.

It is unclear when or if the devices that require up-to-date state information (motion sensors, contact sensors, and camera motion detection) will be available again.

For any additional discussion surrounding this issue I have created a Github Discussion forum here: #232

-----


<a href="https://www.buymeacoffee.com/joshmulliken"><img src="https://img.buymeacoffee.com/button-api/?text=Buy me a coffee&emoji=&slug=joshmulliken&button_colour=FFDD00&font_colour=000000&font_family=Poppins&outline_colour=000000&coffee_colour=ffffff"></a> 

[![Quality Gate Status](https://sonarcloud.io/api/project_badges/measure?project=JoshuaMulliken_ha-wyzeapi&metric=alert_status)](https://sonarcloud.io/dashboard?id=JoshuaMulliken_ha-wyzeapi) [![Visit our IRC channel](https://kiwiirc.com/buttons/irc.libera.chat/wyzeapi.png)](https://kiwiirc.com/client/irc.libera.chat/#wyzeapi) 

# Home Assistant - Wyze Integration

This is a custom component to allow control of various Wyze devices in Home Assistant using the unofficial API. Please
note this mimics the Wyze app and therefore access may be cut off at anytime.

### Highlights of what **WyzeApi** can do

* Control Wyze Bulbs as lights through HA
* Control Wyze Plugs as switches through HA
* Use Wyze Cameras as motion sensors
* Turn on and off Wyze Cameras
* Lock, unlock, and view status of lock and door for the Wyze Lock

### Potential Downsides

* This is an unofficial implementation of the api and therefore may be disabled or broken at anytime by WyzeLabs
* ***It requires two factor authentication to be disabled on your account***

## Funding

If you like what I have done here and want to help I would recommend that you firstly look into supporting Home
Assistant. You can do this by purchasing some swag from their [store](https://teespring.com/stores/home-assistant-store)
or paying for a Nabu Casa subscription. None of this could happen without them.

After you have done that if you feel like my work has been valuable to you I welcome your support through BuyMeACoffee or Github Sponsers in the right hand menu.

## Installation (HACS) - Highly Recommended

1. Have HACS installed, this will allow you to easily update
2. Add [https://github.com/JoshuaMulliken/ha-wyzeapi](https://github.com/JoshuaMulliken/ha-wyzebulb) as a custom
   repository as Type: Integration
3. Click install under "Wyze Bulb and Switch Api Integration" in the Integration tab
4. Restart HA
5. Navigate to _Integrations_ in the config interface.
6. Click _ADD INTEGRATION_
7. Search for _Wyze Home Assistant Integration_
8. Put the email for wyze in the first box and your password in the second
9. Click _SUBMIT_ and profit!

## Usage

* Entities will show up as `light.<friendly name>`, `switch.<friendly name>`, `binary_sensor.<friendly name>`
  or `lock.<friendly name>` for example (`light.livingroom_lamp`).
* Instructions for interacting with lights can be found here: https://www.home-assistant.io/integrations/light/
    * Switches: https://www.home-assistant.io/integrations/switch/
    * Camera motion sensors: https://www.home-assistant.io/integrations/binary_sensor/

## Support

If you need help with anything then please connect with the community!

* Visit us on IRC at librechat in the #wyzeapi channel!
* Visit the discussions tab on this repo
* For bugs or feature requests create an issue
* Check out the [wiki](https://github.com/JoshuaMulliken/ha-wyzeapi/wiki)!

## Reporting an Issue

1. Setup your logger to print debug messages for this component by adding this to your `configuration.yaml`:
    ```yaml
    logger:
     default: warning
     logs:
       custom_components.wyzeapi: debug
       wyzeapy: debug
    ```
2. Restart HA
3. Verify you're still having the issue
4. File an issue in this Github Repository (being sure to fill out every provided field)

