# NS3 video-stream application module

This module is meant to provide a video streaming application for use in NS3 simulations

Based on the work of Guoxi: https://github.com/guoxiliu/VideoStream-NS3
I just made the code work with a newer version of NS3 and refactored the code to be it's own module.

## Installation instructions

Clone this repository into the `contrib` folder of your NS3 installation.

### Basic code usage
```cpp
#include "ns3/video-stream-module.h"

int
main (int argc, char *argv[])
{
    LogComponentEnable ("VideoStreamClientApplication", LOG_LEVEL_INFO);
    LogComponentEnable ("VideoStreamServerApplication", LOG_LEVEL_INFO);

    // TODO: build your topology

    VideoStreamClientHelper videoClient (interfaces.GetAddress (0), 5000);
    ApplicationContainer clientApp = videoClient.Install (nodes.Get (1));
    clientApp.Start (Seconds (0.5));
    clientApp.Stop (Seconds (100.0));

    VideoStreamServerHelper videoServer (5000);
    videoServer.SetAttribute ("MaxPacketSize", UintegerValue (1400));
    videoServer.SetAttribute ("FrameFile", StringValue ("./scratch/frameList.txt"));
    // videoServer.SetAttribute ("FrameSize", UintegerValue (4096));

    ApplicationContainer serverApp = videoServer.Install (nodes.Get (0));
    serverApp.Start (Seconds (0.0));
    serverApp.Stop (Seconds (100.0));

    // TODO: start simulation
}
```

