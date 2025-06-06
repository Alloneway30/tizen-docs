# Attached Devices


You can control attached devices and monitor device changes in your application.

The main features of the device control include the following:

-   Battery information

    You can [get battery details](#battery), such as the current percentage, the charging state, and the current level state.

-   Device control

    You can manage various components and elements on the device:

    -   Display

        You can [get and set display details](#display), such as the number of displays, the maximum brightness of the display, the current brightness, and the display state.

    -   Haptic

        You can [manage haptic devices](#haptic) by, for example, getting the number of haptic devices, opening or closing the haptic handle, and requesting vibration effect playback.

    -   IR

        You can [manage IR devices](#ir) by, for example, determining whether an IR device is available and transmitting an IR pattern.

    -   LED

        You can [manage the camera flash LED](#led) by, for example, getting the maximum and current brightness of the LED. You can also change the current brightness of the camera flash LED, and request the service LED to play effects.

    -   Power

        You can [request the power state](#power) to be locked or unlocked.

-   Change monitoring

    You can [register an event handler to monitor device changes](#changes).

## Prerequisites

To enable your application to use the attached device control functionality, follow the steps below:

1.  To use the [Tizen.System.Display](/application/dotnet/api/TizenFX/latest/api/Tizen.System.Display.html), [Tizen.System.Led](/application/dotnet/api/TizenFX/latest/api/Tizen.System.Led.html), and [Tizen.System.Vibrator](/application/dotnet/api/TizenFX/latest/api/Tizen.System.Vibrator.html) classes, the application has to request permission by adding the following privileges to the `tizen-manifest.xml` file:

    ```XML
    <privileges>
       <!--To use the Display class -->
       <privilege>http://tizen.org/privilege/display</privilege>
       <!--To use the Vibrator class -->
       <privilege>http://tizen.org/privilege/haptic</privilege>
       <!--To use the Led class -->
       <privilege>http://tizen.org/privilege/led</privilege>
    </privileges>
    ```

2.  To use the methods and properties of the [Tizen.System](/application/dotnet/api/TizenFX/latest/api/Tizen.System.html) namespace classes, include the namespace in your application:

    ```csharp
    using Tizen.System;
    ```

## Retrieve battery information

<a name="battery"></a>
To retrieve battery information, follow the steps below:

-   Get the battery charge percentage with the `Percent` property of the [Tizen.System.Battery](/application/dotnet/api/TizenFX/latest/api/Tizen.System.Battery.html) class.

    The property contains the current battery charge percentage as an integer value from 0 to 100 that indicates the remaining battery charge as a percentage of the maximum level:

    ```csharp
    int s_Percent;
    s_Percent = Battery.Percent;
    ```

-   Get the current battery charging state with the `IsCharging` property.

    The property contains the device battery charging state as `TRUE` or `FALSE`:

    ```csharp
    bool charging;
    charging = Battery.IsCharging;
    ```

-   Get the current battery level with the `Level` property.

    The property contains the device battery level as a value of the [Tizen.System.BatteryLevelStatus](/application/dotnet/api/TizenFX/latest/api/Tizen.System.BatteryLevelStatus.html) enumeration:

    ```csharp
    BatteryLevelStatus status;
    status = Battery.Level;
    ```

<a name="display"></a>
## Control the display

To retrieve and set display properties, follow these steps:

-   Get the number of display devices with the `NumberOfDisplays` property of the [Tizen.System.Display](/application/dotnet/api/TizenFX/latest/api/Tizen.System.Display.html) class:

    ```csharp
    int num;
    num = Display.NumberOfDisplays;
    ```

-   Get the maximum possible brightness with the `MaxBrightness` property:

    ```csharp
    Display dis = Display.Displays[0];

    int maxBrightness = dis.MaxBrightness;
    ```

-   Get and set the display brightness with the `Brightness` property:

    ```csharp
    Display dis = Display.Displays[0];

    int curBrightness = 0;
    curBrightness = dis.Brightness;
    dis.Brightness = 30;
    ```

-   Get and set the display state with the `State` property.

    The property contains the display state as a value of the [Tizen.System.DisplayState](/application/dotnet/api/TizenFX/latest/api/Tizen.System.DisplayState.html) enumeration:

    ```csharp
    DisplayState state;
    state = Display.State;
    Display.State = DisplayState.Normal;
    ```

<a name="haptic"></a>
## Control haptic devices

To control haptic devices, follow these steps:

-   Get the number of haptic devices with the `NumberOfVibrators` property of the [Tizen.System.Vibrator](/application/dotnet/api/TizenFX/latest/api/Tizen.System.Vibrator.html) class:

    ```csharp
    int num;
    num = Vibrator.NumberOfVibrators;
    ```

-   Play and stop an effect on a given haptic device with the `Vibrate()` and `Stop()` methods.

    The device vibrates for a specified time with a constant intensity. The effect handle can be 0:

    ```csharp
    Vibrator vib = Vibrator.Vibrators[0];
    vib.Vibrate(3000, 50);

    vib.Stop();
    ```

<a name="ir"></a>
## Control IR devices

To control an IR device, follow these steps:

-   Determine whether IR is available on the device using the `IsAvailable` property of the [Tizen.System.IR](/application/dotnet/api/TizenFX/latest/api/Tizen.System.IR.html) class:

    ```csharp
    bool test;
    test = IR.IsAvailable;
    ```

-   Transmit an IR pattern with a specific carrier frequency using the `Transmit()` method:

    ```csharp
    List<int> pattern = new List<int>();
    pattern.Add(10);
    pattern.Add(50);
    IR.Transmit(10, pattern);
    ```

<a name="led"></a>
## Control LED devices
To control LEDs on the device, follow the steps below:

-   Get the maximum brightness value of a camera flash LED with the `MaxBrightness` property of the [Tizen.System.Led](/application/dotnet/api/TizenFX/latest/api/Tizen.System.Led.html) class:

    ```csharp
    int test;
    test = Led.MaxBrightness;
    ```

-   Get and set the current brightness value of a camera flash LED with the `Brightness` property:

    ```csharp
    int test;
    test = Led.Brightness;

    Led.Brightness = 45;
    ```

-   Play and stop a custom effect on the service LED that is located on the front of the device with the `Play()` and `Stop()` methods:

    ```csharp
    var t = Task.Run(async delegate
    {
        await Task.Delay(1000);

        return 0;
    });

    Led.Play(500, 200, Color.FromRgba(255, 255, 255, 1));
    t.Wait();

    Led.Stop();
    ```

<a name="power"></a>
## Control the power state

To lock and unlock the CPU state, follow the steps below:

-   Lock the power state with the `RequestLock()` method of the [Tizen.System.Power](/application/dotnet/api/TizenFX/latest/api/Tizen.System.Power.html) class.

    The method locks the given PowerLock of the [Tizen.System.PowerLock](/application/dotnet/api/TizenFX/latest/api/Tizen.System.PowerLock.html) enumeration for a specified time. After the given time (in milliseconds), the lock is unlocked. If the process is destroyed, every lock is removed:

    ```csharp
    Power.RequestLock(PowerLock.Cpu, 2000);
    ```

-   Unlock the power state with the `ReleaseLock()` method:

    ```csharp
    Power.ReleaseLock(PowerLock.Cpu);
    ```

<a name="changes"></a>
## Monitor device changes

To monitor device changes, use event handlers registered to the following events:

-   `LevelChanged` and `PercentChanged` events in the [Tizen.System.Battery](/application/dotnet/api/TizenFX/latest/api/Tizen.System.Battery.html) class are called when the battery level and charge percentage change.
-   `ChargingStateChanged` event in the [Tizen.System.Battery](/application/dotnet/api/TizenFX/latest/api/Tizen.System.Battery.html) class is called when the charger is connected or disconnected.
-   `StateChanged` event in the [Tizen.System.Display](/application/dotnet/api/TizenFX/latest/api/Tizen.System.Display.html) class is called when the device display state changes.
-   `BrightnessChanged` event in the [Tizen.System.Led](/application/dotnet/api/TizenFX/latest/api/Tizen.System.Led.html) class is called when LED brightness changes.

To manage device display status change events, follow these steps:

1.  Define an event handler:

    ```csharp
    public static void DisplayEventHandler()
    {
        EventHandler<DisplayStateChangedEventArgs> handler = null;
        handler = (object sender, DisplayStateChangedEventArgs args);
        Log.Debug(LogTag, string.Format("Display State:: {0}", value));
    }
    ```

2.  Register the event handler for the `StateChanged` event of the `Tizen.System.Display` class:

    ```csharp
    Display.StateChanged += handler;
    ```

3.  When no longer needed, deregister the event handler:

    ```csharp
    Display.StateChanged -= handler;
    ```


## Related information
- Dependencies
  -   Tizen 4.0 and Higher
- API References
  - [Tizen.System.Battery](/application/dotnet/api/TizenFX/latest/api/Tizen.System.Battery.html)
  - [Tizen.System.Display](/application/dotnet/api/TizenFX/latest/api/Tizen.System.Display.html)
  - [Tizen.System.Vibrator](/application/dotnet/api/TizenFX/latest/api/Tizen.System.Vibrator.html)
  - [Tizen.System.IR](/application/dotnet/api/TizenFX/latest/api/Tizen.System.IR.html)
  - [Tizen.System.Led](/application/dotnet/api/TizenFX/latest/api/Tizen.System.Led.html)