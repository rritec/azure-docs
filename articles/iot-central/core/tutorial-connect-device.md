---
title: Tutorial - Connect a generic client app to Azure IoT Central | Microsoft Docs
description: This tutorial shows you how to connect a device running either a C, C#, Java, JavaScript, or Python client app to your Azure IoT Central application. You modify the automatically generated device template by adding views that let an operator interact with a connected device.
author: dominicbetts
ms.author: dobett
ms.date: 01/04/2022
ms.topic: tutorial
ms.service: iot-central
services: iot-central
ms.custom: [mqtt, device-developer]
zone_pivot_groups: programming-languages-set-twenty-six

#- id: programming-languages-set-twenty-six
## Owner: dobett
#  title: Programming languages
#  prompt: Choose a programming language
#  pivots:
#  - id: programming-language-ansi-c
#    title: C
#  - id: programming-language-csharp
#    title: C#
#  - id: programming-language-java
#    title: Java
#  - id: programming-language-javascript
#    title: JavaScript
#  - id: programming-language-python
#    title: Python

#Customer intent: As a device developer, I want to try out using device code that uses one of the the Azure IoT device SDKs. I want to understand how to send telemetry from a device, synchronize properties with the device, and control the device using commands.
---

# Tutorial: Create and connect a client application to your Azure IoT Central application

This tutorial shows you how to connect a client application to your Azure IoT Central application. The application simulates the behavior of a temperature controller device. When the application connects to IoT Central, it sends the model ID of the temperature controller device model. IoT Central uses the model ID to retrieve the device model and create a device template for you. You add customizations and views to the device template to enable an operator to interact with a device.

In this tutorial, you learn how to:

> [!div class="checklist"]
> * Create and run the device code and see it connect to your IoT Central application.
> * View the simulated telemetry sent from the device.
> * Add custom views to a device template.
> * Publish the device template.
> * Use a view to manage device properties.
> * Call a command to control the device.

:::zone pivot="programming-language-ansi-c"

[!INCLUDE [iot-central-connect-device-c](../../../includes/iot-central-connect-device-c.md)]

:::zone-end

:::zone pivot="programming-language-csharp"

[!INCLUDE [iot-central-connect-device-csharp](../../../includes/iot-central-connect-device-csharp.md)]

:::zone-end

:::zone pivot="programming-language-java"

[!INCLUDE [iot-central-connect-device-java](../../../includes/iot-central-connect-device-java.md)]

:::zone-end

:::zone pivot="programming-language-javascript"

[!INCLUDE [iot-central-connect-device-nodejs](../../../includes/iot-central-connect-device-nodejs.md)]

:::zone-end

:::zone pivot="programming-language-python"

[!INCLUDE [iot-central-connect-device-python](../../../includes/iot-central-connect-device-python.md)]

:::zone-end

## View raw data

You can use the **Raw data** view to examine the raw data your device is sending to IoT Central:

:::image type="content" source="media/tutorial-connect-device/raw-data.png" alt-text="The raw data view":::

On this view, you can select the columns to display and set a time range to view. The **Unmodeled data** column shows device data that doesn't match any property or telemetry definitions in the device template.

## Clean up resources

[!INCLUDE [iot-central-clean-up-resources](../../../includes/iot-central-clean-up-resources.md)]

## Next steps

If you'd prefer to continue through the set of IoT Central tutorials and learn more about building an IoT Central solution, see:

> [!div class="nextstepaction"]
> [Create a gateway device template](./tutorial-define-gateway-device-type.md)
