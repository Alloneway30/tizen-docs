# Radio

You can control the radio hardware in a device to provide radio playback in your application.

The main features of the `Tizen.Multimedia.Radio` class include the following:

-   Switching the radio on and off

    You can switch the radio on and off using the `Start()` and `Stop()` methods of the `Tizen.Multimedia.Radio` class.

-   Scanning for radio frequencies

    You can [scan for all available frequencies](#scan).

-   Tuning the radio

    You can [select and start playing a radio frequency](#tune) by using the `Frequency` property of the `Tizen.Multimedia.Radio` class.

-   Searching for an adjacent channel

    You can [seek an adjacent channel](#seek) with the `SeekUpAsync()` and `SeekDownAsync()` methods.

You can only have one radio instance active at a time. Radio playback can be interrupted by another radio application.

## Prerequisites


To enable your application to use the radio functionality, proceed as follows:

1.  To use the methods and properties of the [Tizen.Multimedia.Radio](/application/dotnet/api/TizenFX/latest/api/Tizen.Multimedia.Radio.html) class, include the [Tizen.Multimedia](/application/dotnet/api/TizenFX/latest/api/Tizen.Multimedia.html) namespace in your application:

    ```csharp
    using Tizen.Multimedia;
    ```

2.  Create an instance of the `Tizen.Multimedia.Radio` class:

    ```csharp
    Radio radio = new Radio();
    ```

3.  To receive notifications when radio playback is interrupted, register an event handler for the `Interrupted` event of the `Tizen.Multimedia.Radio` class. Radio playback is interrupted, for example, when the radio application moves to the background:

    ```csharp
    radio.Interrupted += OnRadioInterrupted;

    void OnRadioInterrupted(object sender, RadioInterruptedEventArgs args)
    {
        switch (args.Reason)
        {
            case RadioInterruptedReason.ResourceConflict:
                /// Application that was the source of the conflict is now closed
                /// Restart the radio playback here
                break;
            default:
                /// Radio listening is interrupted
                /// Release the application resources or save the current state here
                break;
        }
    }
    ```

<a name="scan"></a>
## Scan for radio frequencies

To scan for all available radio frequencies, proceed as follows:

1.  Register and define event handlers for the events of the [Tizen.Multimedia.Radio](/application/dotnet/api/TizenFX/latest/api/Tizen.Multimedia.Radio.html) class:
    -   To receive a notification each time the scan finds a new frequency, register an event handler for the `ScanUpdated` event. The event provides the kHz value of the found frequency:

        ```csharp
        radio.ScanCompleted += OnScanCompleted;

        void OnScanUpdated(object sender, ScanUpdatedEventArgs args)
        {
            /// Store the radio channels in the array
            /// Frequency values represent the kHz of the channel
            Tizen.Log.Info("Radio", $"Frequency: {args.Frequency}");
        }
        ```

         > [!NOTE]
		 > Do not use radio operations (such as changing the `Frequency` property value or calling the `Start()` method) in the scan updated event handler.


    -   To receive a notification when the scan is complete, register an event handler for the `ScanCompleted` event:

        ```csharp
        radio.ScanCompleted += OnScanCompleted;

        void OnScanCompleted(object sender, EventArgs args)
        {
            /// Frequency scanning is completed
            /// Tune in to one of the scanned frequencies and start listening
        }
        ```

2.  Start scanning using the `StartScan()` method of the `Tizen.Multimedia.Radio` class:

    ```csharp
    radio.StartScan();
    ```

    The scanning time depends on the environment (the strength of the radio signal).

    To cancel the scan before it completes, use the `StopScan()` method.

<a name="tune"></a>
## Tuning the radio

To select and start playing a frequency, proceed as follows:

1.  Set the frequency you want to play using the `Frequency` property of the [Tizen.Multimedia.Radio](/application/dotnet/api/TizenFX/latest/api/Tizen.Multimedia.Radio.html) class:

    ```csharp
    radio.Frequency = newFrequency;
    ```

2.  Start playing the frequency using the `Start()` method of the `Tizen.Multimedia.Radio` class:

    ```csharp
    radio.Start();
    ```

    If the radio emits no sound, check the signal strength with the `SignalStrength` property of the `Tizen.Multimedia.Radio` class. The property returns the current signal strength as a dBuV value.

<a name="seek"></a>
## Search for an adjacent channel

To search for and tune in to an adjacent channel, use the `SeekUpAsync()` and `SeekDownAsync()` methods of the [Tizen.Multimedia.Radio](/application/dotnet/api/TizenFX/latest/api/Tizen.Multimedia.Radio.html) class. This is similar to the scanning operation, but only the nearest active frequency is searched for. Once the maximum frequency is reached in either direction, the search ends, and the radio is set to that frequency.

For example, to seek down, use the `SeekDownAsync()` method:

```csharp
var newFrequency = await radio.SeekDownAsync();

/// Search is complete, and the radio is tuned in to the new frequency
/// Application sets the new frequency and updates the user interface
```

## Related information
* Dependencies
  -   Tizen 4.0 and Higher
