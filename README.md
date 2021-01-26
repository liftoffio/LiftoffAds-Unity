# LiftoffAds Unity SDK

This repository describes the LiftoffAds Unity SDK technical integration.
LiftoffAds Unity SDK currently supports iOS apps using MoPub mediation.

For help configuring and testing ad units or setting up reporting, please
contact your Liftoff POC.

For any other questions, please email sdk@liftoff.io.

## Table of Contents

- [Overview](#overview)
  - [Latest Releases](#latest-releases)
  - [Supported Devices](#supported-devices)
  - [Supported Ad Sizes](#supported-ad-sizes)
  - [Supported Ad Types](#supported-ad-types)
- [Development Requirements](#development-requirements)
- [Integration](#integration)
  - [MoPub Mediation](#mopub-mediation)
    - [MoPub Custom SDK Network](#mopub-custom-sdk-network)

## Overview

### Latest Releases

- [Liftoff MoPub Adapter SDK][latest-mopub]

### Supported Devices

- iPhone
- iPad

### Supported Ad Sizes

- 320x480 (iPhone portrait interstitial)
- 480x320 (iPhone landscape interstitial)
- 768x1024 (iPad portrait interstitial)
- 1024x768 (iPad landscape interstitial)
- 320x50 (iPhone banner)
- 728x90 (iPad banner)
- 300x250 (medium rectangle)

### Supported Ad Types

- HTML and HTML video
- VAST video
- Rewarded

## Development Requirements

The LiftoffAds Unity SDK relies on [External Dependency Manager for Unity](https://github.com/googlesamples/unity-jar-resolver)
to pull in the required iOS dependencies.

To integrate the LiftoffAds Unity SDK, you will need at minimum:

- macOS 10.15.2 or later
- XCode 11.4 or later
- Unity 2018.4 or later
- CocoaPods 1.10.0 or later

## Integration

We currently support MoPub mediation for iOS apps.

### MoPub Mediation

LiftoffAds is a MoPub custom SDK network.

1. Download the [Liftoff MoPub Adapter SDK][latest-mopub].
2. Unzip and import the `.unitypackage` into your project.
3. Initialize MoPub manually with Liftoff as a custom mediated network.
   Make sure to replace the placeholder ad unit ID and API key.
4. After building for iOS, navigate to `Build Settings` and set `Runpath Search
   Paths` to `@executable_path/Frameworks`.

The following code samples may be used as reference for initializing the
LiftoffAds SDK through MoPub. Adjust the logic as necessary to meet the
requirements of your app.

Instructions for initializing and requesting ads through MoPub can be found in the
[MoPub documentation](https://developers.mopub.com/publishers/unity/integrate/).

#### MoPub Custom SDK Network

The custom SDK network option must be selected via MoPub. Additional details
can be found [here](https://github.com/liftoffio/LiftoffAds-iOS#creating-a-mopub-custom-sdk-network).

```csharp
MoPub.InitializeSdk(new MoPub.SdkConfiguration
{
    // Replace MOPUB_AD_UNIT_ID
    AdUnitId = MOPUB_AD_UNIT_ID,
    LogLevel = MoPub.LogLevel.Debug,
    MediatedNetworks = new MoPubBase.MediatedNetwork[]
    {
        // Existing mediation networks ...
        #if UNITY_IOS
        new MoPubBase.MediatedNetwork
        {
            AdapterConfigurationClassName = "LiftoffAdapterConfiguration",
            NetworkConfiguration = new Dictionary<string,string>
            {
                // Replace LIFTOFF_API_KEY with provided API key
                { "apiKey", LIFTOFF_API_KEY },
            },
        }
        #endif
    }
});
```

[latest-mopub]: https://github.com/liftoffio/LiftoffAds-Unity/releases/download/mopub-v1.0.1/LiftoffMoPubAdapter-v1.0.1.zip
