## GOAL

To streamline the process of creating virtual machines using the vagrant boxes provided by Microsoft.

## SETUP

0. Clone the repository, feel free to use the name you want for the destination folder, for example:

    ```sh
    git clone https://github.com/kadimi/wagrant my-win81-ie11
    ```

0. Run **one** of these commands to create the box you want:

    ```sh
    # Default is Windows 7 with IE11
    vagrant up


    # Windows 10
    box_name='msedge.win10.vagrant' vagrant up   # Windows 10 with MSEdge

    # Windows 8.1
    box_name='ie11.win81.vagrant' vagrant up   # Windows 8 with IE11

    # Windows 8
    box_name='ie10.win8.vagrant' vagrant up   # Windows 8 with IE10

    # Windows 7
    box_name='ie8.win7.vagrant' vagrant up   # Windows 7 with IE8
    box_name='ie9.win7.vagrant' vagrant up   # Windows 7 with IE9
    box_name='ie10.win7.vagrant' vagrant up  # Windows 7 with IE10
    box_name='ie11.win7.vagrant' vagrant up  # Windows 7 with IE11 (default)

    # Windows Vista
    box_name='ie7.vista.vagrant' vagrant up     # Windows Vista with IE7

    # Windows XP
    box_name='ie6.xp.vagrant' vagrant up     # Windows XP with IE6
    box_name='ie8.xp.vagrant' vagrant up     # Windows XP with IE8
    ```

0. In the windows machine (the newly created guest), run this command in [a command prompt (aka cmd.exe) with elevated privileges](https://technet.microsoft.com/en-us/library/cc947813(v=ws.10).aspx). Once the set of commands completes, provisioning will be initaited:

    ```sh
    @powershell -NoProfile -ExecutionPolicy Bypass -Command "iex ((new-object net.webclient).DownloadString('https://is.gd/wagrant'))"
    ```

## NOTES

- Some apps are installed during provisioning, you can change that to your liking, see [`ps/Install-Apps.ps1`](https://github.com/kadimi/wagrant/blob/master/ps/Install-Apps.ps1).
- You don't need to provide the `box_name` variable every time, that's only needed with the first `vagrant up`.
- The command `vagrant rdp` may fail, this can be fixed by deleting the line with the faulty fingerprint in `~/.config/freerdp/known-hosts`.

## RESOURCES

- http://stackoverflow.com/a/35721868
- http://support.auvik.com/hc/en-us/articles/204610500-How-to-enable-WMI-monitoring-on-a-single-Windows-device
- https://blogs.msdn.microsoft.com/powershell/2009/04/02/setting-network-location-to-private/
- https://github.com/mitchellh/vagrant/issues/6430
- https://gist.github.com/andreptb/57e388df5e881937e62a
- https://gist.github.com/sneal/39d47401e9eaefcf8727
