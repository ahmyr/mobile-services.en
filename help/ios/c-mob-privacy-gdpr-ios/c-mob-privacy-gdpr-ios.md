---
description: Experience Cloud Mobile SDKs provide General Data Protection Regulation (GDPR)-ready APIs for Controllers that allow users to retrieve locally stored identities and set opt status flags for data collection and transmission.
seo-description: Experience Cloud Mobile SDKs provide General Data Protection Regulation (GDPR)-ready APIs for Controllers that allow users to retrieve locally stored identities and set opt status flags for data collection and transmission.
seo-title: Privacy and General Data Protection Regulation
title: Privacy and General Data Protection Regulation
uuid: 69bb82de-1993-440c-a1b0-8d37919b48b6
---

# Privacy and General Data Protection Regulation {#privacy-and-general-data-protection-regulation}

Experience Cloud Mobile SDKs provide General Data Protection Regulation (GDPR)-ready APIs for Controllers that allow users to retrieve locally stored identities and set opt status flags for data collection and transmission.

>[!IMPORTANT]
>
>GDPR is supported **only** in Mobile SDK version 4.16.0 or later.

When Adobe provides software and services to an enterprise, Adobe acts as a data processor for any personal data it processes and stores as part of providing these services. As a data processor, Adobe processes personal data in accordance with your company’s permission and instructions (for example, as set out in your agreement with Adobe).

As a data controller, you can use Adobe Mobile Services SDKs to support GDPR retrieve and delete requests from your mobile apps.

## New Adobe Experience Cloud SDK Release

Looking for information and documentation related to the Adobe Experience Platform Mobile SDK? Click [here](https://aep-sdks.gitbook.io/docs/) for our latest documentation.

As of September 2018, we released a new, major version of the SDK. These new Adobe Experience Platform Mobile SDKs are configurable through [Experience Platform Launch](https://www.adobe.com/experience-platform/launch.html).

* To get started, go to Launch.
* To see what is in the Experience Platform SDK repositories, go to [Github: Adobe Experience Platform SDKs](https://github.com/Adobe-Marketing-Cloud/acp-sdks).

>[!IMPORTANT]
>
> If you are using the Adobe Experience Platform Mobile SDKs with Adobe Launch, you **must** also install the Adobe Analytics Mobile Services extension to use Adobe Mobile Services features such as in-App messaging, push notifications or Acquisition links. For more information see [Adobe Analytics - Mobile Services](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics-mobile-services).


For the Adobe Mobile SDK portions of your mobile apps, you can use the following settings and methods:

* To retrieve data from the SDKs, and send this data to your servers, use the `getAllIdentifiersAsync` method.

  For more information, see [Retrieving Stored Identifiers](/help/ios/c-mob-privacy-gdpr-ios/c-mob-gdpr-ret-stored-ids-ios.md). 

* To set your opt status and help you with a GDPR data deletion request, use the following settings:

  * `privacyDefault` 
  * `setPrivacyStatus`

  For more information, see [Setting the User's Opt Status](/help/ios/c-mob-privacy-gdpr-ios/privacy.md).

## Additional information {#section_7C7124C50D85469C8C8714533FB1A37D}

* For more information about GDPR, see [GDPR and Your Business](https://www.adobe.com/privacy/general-data-protection-regulation.html). 
* To see the GDPR API documentation, go to [General Data Protection Regulation API](https://adobe.io/apis/cloudplatform/gdpr.html).

