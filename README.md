go.wemo
=======

[![GoDoc](http://godoc.org/github.com/savaki/go.wemo?status.png)](http://godoc.org/github.com/savaki/go.wemo)
[![Build Status](https://snap-ci.com/savaki/go.wemo/branch/master/build_image)](https://snap-ci.com/savaki/go.wemo/branch/master)

Simple package to interface with Belkin wemo devices.

## Standalone Usage Guide

Please utilize the branch [forktest](https://github.com/andrewpurkett/go.wemo/tree/forktest) until a pull request has been submitted for the changes to this library, due to the nature of how go imports libraries.

## Utilizing the library in projects

Here is some example usage of the various functionality incorporated in this go repository:

### Example - Device discovery

```
package main

import (
	"fmt"
	"github.com/savaki/go.wemo"
	"time"
)

func main() {
  api, _ := wemo.NewByInterface("en0")
  devices, _ := api.DiscoverAll(3*time.Second)
  for _, device := range devices {
    fmt.Printf("Found %+v\n", device)
  }
}
```

### Example - Control a device

```
package main

import (
  "fmt"
  "github.com/savaki/go.wemo"
)

func main() {
  // you can either create a device directly OR use the
  // #Discover/#DiscoverAll methods to find devices
  device        := &wemo.Device{Host:"10.0.1.32:49153"}

  // retrieve device info
  deviceInfo, _ := device.FetchDeviceInfo()
  fmt.Printf("Found => %+v\n", deviceInfo)

  // device controls
  device.On()
  device.Off()
  device.Toggle()
  device.BinaryState() // returns 0 or 1
}
```

### Example - Control a named light

As a convenience method, you can control lights through a more generic interface.

```
package main

import (
  "github.com/savaki/go.wemo"
  "time"
)

func main() {
  api, _ := wemo.NewByInterface("en0")
  api.On("Left Light", 3*time.Second)
  api.Off("Left Light", 3*time.Second)
  api.Toggle("Left Light", 3*time.Second)
}
```
