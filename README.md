# Termo ?

I having some hard work to describe it if you have a netter world let me know.

Well its a fridge with a heater inside and they are controlled by a raspberry pie to keep the temp constant.
First task was to keep a perfect temp for making beer but then someone... come up with the ide that is also good for growing plants..

So its can both heat and col the inside of the fridge depending on the needs



## Control
The heater and compressor (for cold) is controlled by power relays thar are connected to a raspberry pi. 
The raspberry then runs a small python script that exposes this as a API (ollebo repos)

The set the time and control the relay Home Assistance is used.

To get a temp inside the fridge a mi plans sensor is set inside the fridge.




![K8s!](/images/1.png)
![K8s!](/images/2.png)
![K8s!](/images/3.png)
![K8s!](/images/4.png)



### fix the fridge
First we need to hack the fridge so we can controll the compressor and a power socket for the heater. 
I hade a compressor that i could by pass the fridge controll and connect a switch dtat started the compressor.
After that a connect some power line and setup a power socket inside the fridge as well for the heatet.

The power cabel where connected to relay to switch on and off the power


### Connect the raspberry
For this a installed a clean raspberry pi image in a new raspberry 3 board. I then connected the relay to gpio pin 17 and 27.
I also setup a 7 screen and mounted the screen on the fridge door.
For termonstad i used a bluetooth my flora stick


### Start
clone this repo and run

```
docker-compose up
```
this will build and start the stack used to monitor the fridge.
The stack has 4 componetes


Login into http://{IP}:8123 with user beer / beer


1. gpio controller
This is a API thet turn the gpio pins up and down and whats control the power sockets

2. mi plant
This will qery all mi devices around and get the data for them and store in a file

3. mi api
This is a api deviced ontop of the mi plant. It reads the file with the data and exposes them over a api endpoint


4. Homeassistace
this is the brain thet controll everything. The gpio pins are added a switch and the mi plant is added as a sensor.
then with simple automations we can have our termo up and running.




#### Config
In the file haconfig/configurations.yaml you have the configurations and you can change to match your gpio pins ore mi plats mac.
To get the mac of ypu miplants let the tool run and look in the logs it will print all devices it finds.


### Build images


![K8s!](/images/s1.jpg)
![K8s!](/images/s2.jpg)
![K8s!](/images/s3.jpg)
![K8s!](/images/s4.jpg)

![K8s!](/images/s4.mp4)