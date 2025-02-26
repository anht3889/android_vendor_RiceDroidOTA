# riceDroid OTA repo
In order for a device to be officially supported by riceDroid, OTA information needs to be added.
Please refer to the following "Readme" to get started

## 1. Introduction ##
In order for a device to be OTA compliant, there are a few things to know.

### 1.1 JSON structure ###
```
{
  "response": [
    {
        "maintainer": "Name (nickname)",
        "oem": "OEM",
        "device": "Device Name",
        "filename": "riceDroid-13.0-<date>-<device codename>-v<riceversion>.zip",
        "download": "https://sourceforge.net/projects/ricedroid/files/<device codename>/<riceversion>/riceDroidAndroid-12.0-<date>-<device codename>-v<riceversion>.zip/download",
        "timestamp": 0000000000,
        "md5": "abcdefg123456",
        "sha256": "abcdefg123456",
        "size": 123456789,
        "version": "<riceversion>",
        "buildtype": "Test/Alpha/Beta/Nightly/Weekly/Monthly",
        "forum": "https://forum link",
        "gapps": "https://gapps link",
        "firmware": "https://firmware link",
        "modem": "https://modem link",
        "bootloader": "https://bootloader link",
        "recovery": "https://recovery link",
        "paypal": "https://donation link",
        "telegram": "https://telegram link",
        "dt": "https://github.com/ricedroidandroid/android_device_<oem>_<device_codename>",
        "common-dt": "https://github.com/ricedroidandroid/android_device_<orm>_<SOC>-common",
        "kernel": "https://github.com/ricedroidandroid/android_kernel_<oem>_<SOC>"
    }
  ]
}
```

### 1.2 changelog.txt structure ### 
```
Highlights & Device Specific Changes:
Build type: Testing/Alpha/Beta/Weekly/Monthly
Device: Device name (<device codename>)
Device maintainer: Name (nickname)
Required firmware: add if any else remove this line

===== <date> =====
- change 1
- change 2
- change 3
```

## 2 Guidelines ##
* Check if your device has all [requirements](https://github.com/ricedroidandroid/rules-and-guidelines#builds-quality-requirements) to be officially supported
* Check if manufacturer already exists
* Check if published link is official
* Check if JSON is intact with help of online validator tools like [https://jsonformatter.curiousconcept.com](https://jsonformatter.curiousconcept.com) or [https://jsonformatter.org](https://jsonformatter.org)
* Check if no extra / missing spaces

## 3. How to ##
For following below description, replace *codename* with your device codename. 
### 3.1 Initial support ###
After getting approval from OTA repository maintainer(s) via maintainer's group, follow the steps below.
1. Fork this repo to your own GitHub
2. Copy file **createjson.sh** from *initial support* folder to riceDroid source folder and make it executable
```
chmod +x createjson.sh
```
3. Open the file in a text editor (vim, nano, any GUI editor) and make changes from where it states *#modify values below*, save the file then run the generation script with below command
```
./createjson.sh
```
4. A file named *codename*.json gets created in main riceDroid source folder. Copy it to where this repo was cloned.
5. Create a file named changelog_*codename*.txt based on changelog structure from point 1.2, and add your changelog in it.
6. Submit a pull request to this repo (this way we validate that you understood the requirements and if all is good you'll be granted direct push access to this repo)

### 3.2 Update build ###
1. Clone this repo locally
```
git clone https://github.com/RiceDroid/android_vendor_RiceDroidOTA -b thirteen
```
2. Change to the directory where you cloned this repo (android_vendor_RiceDroidOTA) and fetch updates from repo.
```
cd android_vendor_RiceDroidOTA
git fetch --all
git pull
```
3. Copy *codename*.json file from out dir (where your riceDroid zip is compiled) over to this repo folder (android_vendor_RiceDroidOTA).
4. Make changes to changelog_*codename*.txt and save it.
5. Now with the files updated, commit your update to this repo.
```
git add .
git commit #(this opens up your prefered text editor, so write a nice description like "<device codename>: update build")
git push #you may be prompted for your github username and password
```
