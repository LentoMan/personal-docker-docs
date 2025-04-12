# Browser safety
Your browser could potentially leak or exfiltrate data to the internet using javascrip, turning off javascript is usually not an option as it may break the application. 

An easy fix is to use Firefox in offline mode which is described in the section below. Some other options to explore would be either using a software firewall to block external traffic for the browser executable or configuring a secure local proxy in your browser.

## Firefox Offline Mode
, an easy fix is to use Firefox with the `Work Offline` option. After starting Firefox, press `Alt` or `F10`, then select `Work Offline` from the file menu. You will still be able to access localhost but there should be no external internet access. You may also want to open developer mode with `F12` to monitor the **Console** and **Network** tabs for potential issues when working offline. Some remote dependencies may be loaded from content delivery networks, but can often be cached before working offline.

When using offline mode, you may run into browser issues with things like dropdowns not updating with latest added models etc., consider turning off disk cache or clearing browser cache if that happens. It may be a good idea to create a separate Firefox profile without disk cache which always starts in offline mode.

## Creating an Offline Profile (Windows)

In order to create a separate firefox profile using Windows, place a shortcut to Firefox on your desktop or duplicate the existing shortcut, rename the copy to `altprofile`. Right click the `altprofile` shortcut and open the properties, change the target to something like:
```
"C:\Program Files\Mozilla Firefox\firefox.exe" -profile "E:\altprofile" -no-remote -offline
```

The `-no-remote` option is important, it allows you to use multiple profiles like your **default profile** and your **altprofile** independently at the same time in different windows. Launch the **altprofile** shortcut and make sure it starts offline. You may now also want to disable any diagnostics, telemetry and crash reports in the Firefox security settings for your alternative profile.

The new profile should be hidden from the profilemanager, but in case your default firefox profile no longer opens as default, open the profilemanager and set it as default without asking using:
```
"C:\Program Files\Mozilla Firefox\firefox.exe" -profilemanager
```

**Do not delete any profiles in the profilemanager as it may delete your default profile along with the actual profile you wanted to delete.**

To turn of disk cache, enter `about:config` in the url bar and accept the risk. Next, search for `browser.cache.disk.enable` and toggle it to false. To verify that the setting is applied, enter `about:cache` in the url bar. The **Storage disk location** should now say "**none, only stored in memory**".
