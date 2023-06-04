# Custom Element iOS

## Initialize TEAM_ID

1. go to your [developer account](https://developer.apple.com/account)
2. look for **Membership details**
3. copy **Team ID** to *TEAM_ID* secret of repository

## Initialize HOMESERVER

1. create *HOMESERVER* secret with your own server that you want to use instead of default `matrix.org`

## Initialize BUNDLE_DISPLAY_NAME

1. create *BUNDLE_DISPLAY_NAME* secret and provide name that will be shown on iPhone screen

## Create Apple distribution certificate

here we create Apple distribution certificate and initialize *DISTRIBUTION_CERTIFICATE_NAME*, *CERTIFICATE_P12* and *CERTIFICATE_P12_PASSWORD* secrets of repository

1.	Launch **Keychain Access** located in **/Applications/Utilities** on your MAC.
2.	Choose **Keychain Access > Certificate Assistant > Request a Certificate** from a **Certificate Authority**.
3.	In the **Certificate Assistant** dialog, enter an email address in the **User Email Address** field.
4.	In the **Common Name** field, enter a name for the key. 
5.	Leave the **CA Email Address** field empty.
6.	Choose **Saved to disk**, then click **Continue**.
7.	Click **Continue** and go back to your browser
8.	In [Certificates, Identifiers & Profiles](https://developer.apple.com/account/resources/certificates/list), click Certificates in the sidebar.
9.	On the top left, click the add button **(+)**.
10.	Select **Apple Distribution**, then click **Continue**.
12.	Click **Choose File**.
13.	In the dialog that appears, select the certificate request file, which we have recently created (a file with a `.certSigningRequest` file extension), then click **Choose/Open**.
14.	Click **Continue**.
15.	Click **Download** and then save.
16.	The certificate file (a file with a `.cer` file extension) appears in your Downloads folder, double-click it to install in your **Keychain Access**
17.	Start **Keychain Access**.
18.	On the top left sidebar select **login** and on the bottom left select **My Certificates**.
19.	This will list all your installed certificates and the associated private key.
20. Find distribution certificate that we have recently created
21. Copy it's name to *DISTRIBUTION_CERTIFICATE_NAME* secret of your repository
22.	Select private key of this certificate and choose **Export** from the pop-up menu. 
21.	Enter **name** at save as, then click **Create**
22.	Enter **password** (and copy it to *CERTIFICATE_P12_PASSWORD* secret of your repository)
23. you get your distribution certificate in .`p12` format
24. open terminal
25. run command `base64 [/path/to/your/p12/certificate]` and copy the resulting line to *CERTIFICATE_P12* secret of your repository

## Creating an App Store Connect API Key

Here we create a new **App Store Connect API Key** and initialize *APPSTORECONNECT_KEY_ID*, *APPSTORECONNECT_KEY_ISSUER_ID* and *APPSTORECONNECT_KEY_CONTENT* secrets of repository

1. open [Users and Access page](https://appstoreconnect.apple.com/access/users)
2.	Select the **Keys** tab
3.	You will see **Issuer ID**, copy it to *APPSTORECONNECT_KEY_ISSUER_ID* secret of your repository
4.	Click on the **(+)** button
5.	Provide **Name** and select **App Manager** role
6.	Download the newly created **API Key file** (`.p8`). This file cannot be downloaded again after the page has been refreshed
7.	You will see **Key Id** of the Api Key that we have recently created, copy it to *APPSTORECONNECT_KEY_ID* secret of your repository
8. open `.p8` file in Downloads folder in text editor program
9. add `\n` after `-----BEGIN PRIVATE KEY-----` and before `-----END PRIVATE KEY-----` and copy result string (it'd look like `-----BEGIN EC PRIVATE KEY-----\nfewfawefawfe\n-----END EC PRIVATE KEY-----`) to *APPSTORECONNECT_KEY_CONTENT* secret of your repository

## Create App Group

Here we create App Group and initialize *GROUP_ID* secret of repository

1. go to **Identifiers** in [Certificates, Identifiers & Profiles](https://developer.apple.com/account/resources/identifiers/list)
2. click on **plus** button
3. choose **App Groups** and click **Continue**
4. provide description
5. provide ID of group (something like `group.im.vector` in original Element) and copy it to *GROUP_ID* secret of your repository
6. click **Continue**

## Create iCloud Container

1. go to **Identifiers** in [Certificates, Identifiers & Profiles](https://developer.apple.com/account/resources/identifiers/list/cloudContainer)
2. choose list of iCloud Containers (right upper corner)
3. click on **plus** button
4. choose **iCloud Containers** and click **Continue**
5. provide description (something like: Element iCloud Container)
6. write `iCloud.[base_app_id]` as bundleID (change `[base_app_id]` to your future app_id (we will create it later))
7. click **Continue**
8. click **Register**

## Create Base App ID

here we initialize *BASE_BUNDLE_IDENTIFIER* secret

1. go to **Identifiers** in [Certificates, Identifiers & Profiles](https://developer.apple.com/account/resources/identifiers/list)
2. click on **plus** button
3. choose **App IDs** and click **Continue**
4. select **App** type and click **Continue**
5. provide description
6. choose **explicit** for bundle ID and enter it (`[base_app_id]` that we mentioned earlier)
7. copy bundle ID to *BASE_BUNDLE_IDENTIFIER* secret of your repository
8. select **Capabilities**
9. enable **ICloud** (with **Include CloudKit support**), then click **Edit**, select iCloud container that you have created (`iCloud.[base_app_id]`) and click **Continue**
10. enable **SiriKit**, **associated-domains** and **push notifications**
11. enable **App Groups** from **Capabilities** 
12. for **App Groups** click **Edit** button and choose a newly created group, then click **Continue**, click **Save**
13. click **Continue**
14. click **Register**

## Create App ID for Share Extension and Siri Intents

You should do it 2 times for each of Extensions: Share Extension and Siri Intents Extension

1. go to **Identifiers** in [Certificates, Identifiers & Profiles](https://developer.apple.com/account/resources/identifiers/list)
2. click on **plus** button
3. choose **App IDs** and click **Continue**
4. select **App** type and click **Continue**
5. provide description
6. choose **explicit** for bundle ID and enter it `([base_app_id].shareExtension, dev.[base_app_id].SiriIntents for Share Extension and Siri Intents Extension respectively)` 
7. choose **App Groups** from **Capabilities**
8. for **App Groups** click **Edit** button and choose a newly created group, then click **Continue**, click **Save**
9. click **Continue**
10. click **Register**

## Create App ID for NSE

1. go to **Identifiers** in [Certificates, Identifiers & Profiles](https://developer.apple.com/account/resources/identifiers/list)
2. click on **plus** button
3. choose **App IDs** and click **Continue**
4. select **App** type and click **Continue**
5. provide description
6. choose **explicit** for bundle ID and `[base_app_id].nse` 
7. select **Capabilities**
8. enable **App Groups** 
9. for **App Groups** click **Edit** button and choose a newly created group, then click **Continue**, click **Save**
10. select **Additional Capabilities** 
11. enable **Notification (NSE) Filtering**
12. click **Continue**
13. click **Register**

## Create Provisioning Profiles

You should do it 4 times for our app and each of Extensions: Share Extension, Siri Intents Extension and NSE

here we initialize *MAIN_PROVISIONING_PROFILE_NAME*, *SHARE_EXTENSION_PROVISIONING_PROFILE_NAME*, *SIRI_INTENTS_PROVISIONING_PROFILE_NAME* and *NSE_PROVISIONING_PROFILE_NAME* secrets

1. go to **Profiles** in [Certificates, Identifiers & Profiles](https://developer.apple.com/account/resources/profiles/list)
2. click on **plus** button
3. from **Distribution** choose **App Store** and click **Continue**
4. choose **App ID** `([base_app_id], [base_app_id].shareExtension, [base_app_id].SiriIntents, [base_app_id].nse for App, Share Extension, Siri Intents Extension and NSE respectively)` and click **Continue**
5. select distribution certificate that we create recently and click **Continue**
6. provide **Name**  (somethink like `Element App_Name [Name_of_extension]`) and copy it to *MAIN_PROVISIONING_PROFILE_NAME*, *SHARE_EXTENSION_PROVISIONING_PROFILE_NAME*, *SIRI_INTENTS_PROVISIONING_PROFILE_NAME* and *NSE_PROVISIONING_PROFILE_NAME* secrets of your repository for App, Share Extension, Siri Intents Extension and NSE respectively
7. click **Generate**

## Send information about app for enable encryption

Requirenments:
1. email should be send to both `crypt-supp8@bis.doc.gov` and `enc@nsa.gov`
2. email subject should be `Self-Classification Report for Encryption Items`
3. the body of email should be left blank
4. email should contain `.csv` file with information for following 12 points:
```
PRODUCT NAME, MODEL NUMBER, MANUFACTURER, ECCN, AUTHORIZATION TYPE, ITEM TYPE, SUBMITTER NAME, TELEPHONE NUMBER, E-MAIL ADDRESS, MAILING ADDRESS, NON-U.S. COMPONENTS, NON-U.S. MANUFACTURING LOCATIONS
```

## Enable encryption at App Store Connect

1. go to [App Store Connect](https://appstoreconnect.apple.com)
2. From **My Apps**, select your app. The page opens with the App Store tab selected.
3. Click the **Services** tab, and in the sidebar, click **Encryption**.
4. Click the **add** button (+).
5. You should answer on several questions:
    1. Does your app use encryption? Yes
    2. Does your app qualify for any of the exemptions provided in Category 5, Part 2 of the U.S. Export Administration Regulations? Yes
    3. Click **Start Internal Testing**

## Add Test Information

1. go to [App Store Connect](https://appstoreconnect.apple.com)
2. From **My Apps**, select your app. The page opens with the App Store tab selected.
3. Click the **Testflight** tab, and in the sidebar, under **General Information**, click **Test Information**.
4. On the right, choose **English** language
5. In the **Beta App Description** text field, enter a description of your beta version.
6. In the **Feedback Email** field, enter the email address that testers can use to contact you through the TestFlight app. This is also the reply-to address in email invitations to testers.
7. In **Beta App Review Information** provide **Contact Information** (all fields)
8. Click on **Sign-in required** and add information about **Demo account** (login and password)

## Comment about the warning message in the mail

after deploying the application to the app store connect, you'll get email with the following content:

```
Dear Developer,
We identified one or more issues with a recent delivery for your app, "[Name of APP]". Your delivery was successful, but you may wish to correct the following issues in your next delivery:
ITMS-90626: Invalid Siri Support - No example phrase was provided for INStartAudioCallIntent in the 'ru' language. Please refer to 'https://developer.apple.com/documentation/sirikit /registering_custom_vocabulary_with_sirikit/global_vocabulary_reference/intent_phrases'
ITMS-90626: Invalid Siri Support - No example phrase was provided for INSendMessageIntent in the
'de' language. Please refer to 'https://developer.apple.com/documentation/sirikit /registering_custom_vocabulary_with_sirikit/global_vocabulary_reference/intent_phrases"
... (a lot of such strings)
```

> receiving this warning message is not a stopper for the deployment

It can be solved by providing example phrases for each of these three intents: **INStartAudioCallIntent**, **INStartVideoCallIntent** and **INSendMessageIntent**. `AppIntentVocabulary.plist` file (example [here](https://gist.github.com/mitch2be/6e49d5e07e567bbc4d049bc565dad473)) with example phrases should be added to the appropriate `.lproj` folder for each of the languages in [this folder](https://github.com/vector-im/element-ios/tree/c87b8e25e136f68e0187b295613db9d836fa065a/Riot/Assets) of original element-ios