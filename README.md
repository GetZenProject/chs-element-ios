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
10. enable **Siri**, **associated-domains** and **push notifications** ДОБАВИТЬ СЮДА ВЫБОР ICLOUD
11. enable **App Groups** from **Capabilities** ДОБАВИТЬ СЮДА ВЫБОР СОЗДАННОЙ ГРУППЫ
12. click **Continue**

## Create App ID for Share Extension and Siri Intents

You should do it 2 times for each of Extensions: Share Extension and Siri Intents Extension

1. go to **Identifiers** in [Certificates, Identifiers & Profiles](https://developer.apple.com/account/resources/identifiers/list)
2. click on **plus** button
3. choose **App IDs** and click **Continue**
4. select **App** type and click **Continue**
5. provide description
6. choose **explicit** for bundle ID and enter it `([base_app_id].shareExtension, dev.[base_app_id].SiriIntents for Share Extension and Siri Intents Extension respectively)` 
7. choose **App Groups** from **Capabilities** ДОБАВИТЬ СЮДА ВЫБОР СОЗДАННОЙ ГРУППЫ
8. click **Continue**

## Create App ID for NSE

1. go to **Identifiers** in [Certificates, Identifiers & Profiles](https://developer.apple.com/account/resources/identifiers/list)
2. click on **plus** button
3. choose **App IDs** and click **Continue**
4. select **App** type and click **Continue**
5. provide description
6. choose **explicit** for bundle ID and `[base_app_id].nse` 
7. select **Capabilities**
8. enable **App Groups** ДОБАВИТЬ СЮДА ВЫБОР СОЗДАННОЙ ГРУППЫ
9. select **Additional Capabilities** 
10. enable **Notification (NSE) Filtering**
11. click **Continue**

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
