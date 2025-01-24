# Problem

Some apps experience parsing problems during installation, leading to failures.

In my specific case, I encountered an issue installing the 'Blue Archive' app from the 'One Store' app store on 2025-01-23. Your experience may differ depending on your device and configuration.

# Cause

Xiaomi smartphones come with MIUI, which uses `com.miui.global.packageinstaller` as the default package installer.

I believe this incompatibility with certain apps, particularly their APK files, is the root cause of the issue.

# Forewarning

## Consider Other Solutions First

My solution in the next section is intended as a last resort after exhausting all other options.

One potential alternative is disabling MIUI optimization in developer mode, which has worked for some users but may reset certain settings, like keyboard preferences.[1] However, disable MIUI optimization was unavailable on my Xiaomi 13 global.

## Potential Security Risks

Note that enabling USB debugging and using ADB commands may pose security risks. To minimize risks, ensure USB debugging is disabled once you’ve completed the process, and only connect to trusted and secure machines.

# My Solution: What Worked for Me

The following solution is what ultimately worked for me to resolve the app parsing issue. Keep in mind that your experience may vary depending on your device and configuration.

This solution was implemented on a Windows system but is compatible with macOS and Linux as well.

1. **Prepare Resources**: Use this website, [XDA Developers](https://www.xda-developers.com/uninstall-carrier-oem-bloatware-without-root-access/)[2], and follow the detailed instructions provided there up until the step to locate the package you want to uninstall.
2. **Uninstall the Xiaomi Package Installer**:
Use the following command to uninstall the Xiaomi package installer:

    ```bash
    pm uninstall -k --user 0 com.miui.global.packageinstaller
    
    ```

3. **Reinstall Your App Store**:
This step is necessary because it will try to use miui package installer if not reinstalled.
4. **Restart your smartphone**:

    First thing to do when messing with settings.

5. **Retry App Installation**:

    Attempt to install your desired app.

6. **Additional Steps if the Above Doesn't Work**:
    - **Note: No Root Required**
    Despite said website[2] stating that rooting is necessary, I successfully performed following steps without rooting my device, however your case may differ.
    - Fully uninstall the Xiaomi package installer using the command:

        ```bash
        pm uninstall com.miui.global.packageinstaller
        ```

    - Reinstall your app store again.
    - Restart your smartphone.

After this, I was able to install my app without encountering parsing errors.

# Resources

[1] https://namu.wiki/w/%EC%9B%90%EC%8A%A4%ED%86%A0%EC%96%B4

[2] https://www.xda-developers.com/uninstall-carrier-oem-bloatware-without-root-access/