# cue_sdk
Python wrapper for the CUE SDK

[On PyPi](https://pypi.python.org/pypi/cue_sdk/)

# Installation
Use pip
```python
>>> pip install cue_sdk
```

# Usage example
```python
>>> from cue_sdk import *
# Load CUE DLL. Provide path to DLL yourself.
>>> Corsair = CUE("CUESDK.x64_2013.dll")
# Gives us exclusive access to controling the lighting and turns everything off.
>>> Corsair.RequestControl(CAM.ExclusiveLightingControl)
True
# Sets the color of the H key to white.
>>> Corsair.SetLedsColors(CorsairLedColor(CLK.H, 255, 255, 255))
True
# Sets the color of the A and B key to green
Corsair.SetLedsColors([CorsairLedColor(CLK.A, 0, 255, 0), CorsairLedColor(CLK.B, 0, 255, 0)])
# Returns number of Corsair devices.
>>> Corsair.GetDeviceCount()
1
# Takes zero-based index of device and returns a namedtuple with the device info.
>>> device_info = Corsair.GetDeviceInfo(0)
>>> print(device_info)
CorsairDeviceInfo(type=<CDT.Keyboard: 2>, model='K70 RGB', physicalLayout=<CPL.US: 1>, logicalLayout=<CLL.NA: 2>, capsMask=<CDC.Lighting: 1>)
# Takes zero-based index of device and returns a namedtuple with the led positions + led count.
>>> Corsair.GetLedPositions(0) 
CorsairLedPositions(numberOfLed=111, pLedPosition=[CorsairLedPosition(ledId=13, top=50.0, left=7.0, height=13.0, width=13.0), ...])
# Returns the led id (CLK enum) for the key name. Relative to logical layout (e.g. on an AZERTY keyboard it will return Q, not A)
>>> Corsair.CorsairGetLedIdForKeyName('a')
<CLK.A: 38>
# Performs protocol handshake and returns details. Already called when the CUE class is initialized, no need to call for it yourself. 
>>> Corsair.PerformProtocolHandshake()
CorsairProtocolDetails(sdkVersion='1.15.28', serverVersion='1.16.42', sdkProtocolVersion=2, serverProtocolVersion=2, breakingChanges=False)
# Protocol details are stored here when called handshake is performed on init.
>>> Corsair.ProtocolDetails
CorsairProtocolDetails(sdkVersion='1.15.28', serverVersion='1.16.42', sdkProtocolVersion=2, serverProtocolVersion=2, breakingChanges=False)
```
