# NetRestore/NetInstall configuration

- Configuration info for packages to install/image to restore is found in `NetInstall/Packages/InstallPreferences.plist`
## Important keys in InstallPreferences
|Key Name|Type|Values|Description|
|--------|----|------|-----------|
|`descriptionKey`|String|Any|A plaintext, human readable description of the image to be installed.|
|`sourceKey`|String|Any|URL to the image that asr will connect to when NetRestoring|
|`sourcePath`|String|Any|Path in the DMG to the image to be restored|
|`restoreSourcesBrowseMulticast`|Boolean|True/False|True allows multicast imaging from a server|
|`installRecoveryPartition`|Boolean|True/False|Install recovery partition, or not.|
|`restoreSourcesAllowManual`|Boolean|True/False|Allows manual entry of image source|
|`restoreSourceBrowseOthers`|Boolean|True/False|Use Bonjour to find another image source|
|`restoreSourcesArray`|Array of strings|Any|Not filled if you choose a local path with `sourcePath`|

## Important keys in NBImageInfo.plist
|Key Name|Type|Values|Description|
|`SupportsDiskless`|Boolean|True/False|Allow running from diskless systems (i.e. don't use local swap on internal drive|
|`RootPath`|String|Any|The path to NetInstall.dmg|
|`ImageType`|String|NetRestore/NetInstall|Depends on how you've configured the image|
|`DisabledSystemIdentifers`|Array of String|Any|Disables certain models of Mac from NetBooting to this server|

## Files in `/var/db`

|File|Description|
|----|-----------|
|`.AppleSetupDone`|Created on completion of Setup Assistant. Remove to skip login window and create a new admin account.|
|`.RunLanguageChooserToo`|If exists, allows user to change language of Setup Assistant, otherwise it follows the installer language|