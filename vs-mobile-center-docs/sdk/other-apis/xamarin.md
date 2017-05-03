---
title: Other Xamarin APIs
description: Other APIs in the Mobile Center SDK for Xamarin
keywords: sdk
author: elamalani
ms.author: emalani
ms.date: 04/17/2017
ms.topic: article
ms.assetid: 64f8592a-73e0-4f08-9c29-4de82e2d1131
ms.service: mobile-center
ms.custom: sdk
ms.tgt_pltfrm: xamarin
---

# Other Xamarin APIs

> [!div class="op_single_selector"]
> * [Android](android.md)
> * [iOS](ios.md)
> * [React Native](react-native.md)
> * [UWP](uwp.md)
> * [Xamarin](xamarin.md)

## Adjust the log level

You can control the amount of log messages that show up from Mobile Center in the console. Use the `LogLevel`-API to enable additional logging while debugging. By default, it is set to `ASSERT` for the App Store environments and `WARN` otherwise.

To have as many log messages as possible, use `LogLevel.Verbose`.

```csharp
MobileCenter.LogLevel = LogLevel.Verbose;
```

## Identify installations

The Mobile Center SDK creates a UUID for each device once the app is installed. This identifier remains the same for a device when the app is updated and a new one is generated only when the app is re-installed. The following API is useful for debugging purposes.

```csharp
System.Guid installId = MobileCenter.InstallId;
```

## Disable all services at runtime

If you want to disable all Mobile Center services at once, use the `Enabled`-property. When disabled, the SDK will not forward any information to Mobile Center.

```csharp
MobileCenter.Enabled = false;
```

To enable all services at once again, use the same API but pass `true` as a parameter.

```csharp
MobileCenter.Enabled = true;
```
