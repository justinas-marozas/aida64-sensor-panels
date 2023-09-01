# Info overload

See all the stats!

![photo](./photo.JPG)

## The PC

- 16 core 32 thread CPU, AM4, AMD
- 4 sticks of memory, DDR4, G-Skill
- 2 NVMe SSDs, Samsung
- GPU, PCIe4, Nvidia, EVGA
- Motherboard, ASUS
- Custom watercooling loop
    - Temperature sensor connected to Water In header, EKWB
    - Temperature sensor connected to Water Out header, EKWB
    - Fans, all controlled through the same PWM header, EKWB
    - Water pump connected to Water Pump header
    - (no water flow sensor, sadly)

CPU fan header is not connected and the Sensor Panel is not configured to show it. I no longer remember why I connected the fans to a random chasis fan header and not the CPU fan header. Maybe BIOS wouldn't let me control the CPU fan curve based on water temperatures? Must be something like that as BIOS freaks out if it doesn't detect a CPU fan and I had to tell bios to ignore it or it wouldn't load the OS and who would deal with that if they could avoid it.

## The sensor panel

- Fills a 7" Raspberry Pi display (1024x600 resolution)
- Shows TIME
- Shows clock of each CPU core (16) and utilisation of each thread (32)
- Show water in and water out temperatures
- Shows temparature of pretty much every component I could fit on the display
- Shows game FPS graph

### How to set it up

Install [Aida64](https://www.aida64.com/downloads) (it is **not** a free software) (I'm using Aida64 Extreme)

Launch Aida64. In the top menu, go to File / Preferences, and:
- Go to General
    - ☑ Load AIDA64 at Windows startup (Sensor Panel only works while Aida64 is running)
- Go to Sensor Panel
    - ☑ Show SensorPanel (to show the panel with all the info that we'll configure later)
    - ☑ Enable context menu (I right-click the panel to load the Sensor Panel Manager)
- Go to Stability
    - ☑ DIMM thermal sensor support (to make memory stick temperatures show [[1]](https://forums.aida64.com/topic/1376-ram-temperature-monitoring/?do=findComment&comment=7822) [[2]](https://forums.aida64.com/topic/7534-ram-temps-not-showing-up-in-sensor-data/?do=findComment&comment=31886))
    - ☑ Embedded controller (EC) support (to make water temperatures show [[3]](https://forums.aida64.com/topic/7437-water-in-and-water-out-sensors-asus-crosshair-viii-dark-hero-asus-maximus-xii-apex/?do=findComment&comment=31425))
    - ☑ Embedded controller (EC) bank switching (to make water temperatures show [[3]](https://forums.aida64.com/topic/7437-water-in-and-water-out-sensors-asus-crosshair-viii-dark-hero-asus-maximus-xii-apex/?do=findComment&comment=31425))

You should have a rectangle with some default fields floating around. That is the sensor panel. Right-click it and Select SensorPanel Manager. In the Popup click Import and navigate to the [info-overload.sensorpanel](./info-overload.sensorpanel) (in this directory).

Install [MSI Afterburner](https://www.msi.com/Landing/afterburner/graphics-cards) and:
- **In the install wizzard** make sure that RivaTunner Statistics Server (RTSS) is selected. Game FPS won't work without it
- Set MSI Afterburner to start with Windows (I'm _almost_ certain it is required)
- Set MSI Afterburner to start minimised to system tray. I don't need to see it
- Set RTSS to start with Windows (the panel starts with Windows and the FPS graph won't work without RTSS running)
- Set RTSS to start minimised to system tray. I don't need to see it

Restart the PC.

### Troubleshooting

#### FPS graph just tracks 0

Are you playing a game? It only tracks when full-screen something something is running. And I noticed in some games it only starts tracking when I'm done clicking in the menu and proper 3D enviromnent is loaded.

Is RivaTunner Statistics Server (RTSS) running? You should see it in the system tray. The icon is a monitor with blue background and red numbers.

Is MSI Afterburner running? I'm not certain it's required as the sensor panel only cares about RTSS, but maybe RTSS cares about MSI Afterburner?

Did you restart the PC after installing RTSS? FPS didn't work until I restarted the PC.

#### Fan speed shows N/A

What motherboard header are you using? The panel is configured to track Chasis fan #2 as that's where my fan controller is connected. Check what fan headers you are using, open SensorPanel Manager (right-click), and change the field to track the correct sensor.

#### Water in and water out shows N/A

Did you configure Aida64? Check the stability section above.

Do you have water temp sensors in your rig? How are they connected? Do you see the temperatures in the BIOS?

#### RAM temperatures shows N/A

Did you configure Aida64? Check the stability section above.

Do your RAM sticks have temperature sensors?

Do you see all four as N/A? If you only have two sticks, I assume you'd see two N/As. Go to the SensorPanel Manager (right-click) and remove the fields for the ones not connected.

#### I opened Aida64 and it's in the tiny display and it's annoying

Yep. Aida64 windows open on the the screen running the sensor panel. It's annoying. I just drag the panel to the main screen before interacting with Aida64. Less annoying.

#### I opened SensorPanel Manager and it's in the tiny display and it's annoying

Same as above.

#### I rearranged displays in Windows settings and my sensor panel is gone

It remembers its location relative to the main screen. You'll have to go back to windows settings and move some display back the where the panel was, save the settings, drag the panel to the main screen, rearrange your screens in Windows settings again, and _then_ drag the sensor panel to the secondary screen you prefer.
