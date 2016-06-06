## SETUP

0. Clone the repository, feel free to use the name you want for the destination folder, for example:

    ```sh
    git clone https://github.com/kadimi/wagrant my-win81-ie11
    ```

0. Run **one** of these commands to create the box you want:

    ```sh
    vagrant up                           # Windows 7 with IE11
    box_name='win7-ie10' vagrant up      # Windows 7 with IE10 
    box_name='win7-ie9' vagrant up       # Windows 7 with IE9 
    box_name='win7-ie8' vagrant up       # Windows 7 with IE8 
    box_name='win8-ie10' vagrant up      # Windows 8 with IE10 
    box_name='win81-ie11' vagrant up     # Windows 8 with IE11 
    ```

0. In the windows machine (the newly created guest), run this command in [a command prompt (aka cmd.exe) with elevated privileges](https://technet.microsoft.com/en-us/library/cc947813(v=ws.10).aspx):

    ```sh
    @powershell -NoProfile -ExecutionPolicy Bypass -Command "iex ((new-object net.webclient).DownloadString('https://is.gd/wagrant'))"
    ```

## RESOURCES

- http://stackoverflow.com/a/35721868
- http://support.auvik.com/hc/en-us/articles/204610500-How-to-enable-WMI-monitoring-on-a-single-Windows-device
- https://blogs.msdn.microsoft.com/powershell/2009/04/02/setting-network-location-to-private/
- https://github.com/mitchellh/vagrant/issues/6430
- https://gist.github.com/andreptb/57e388df5e881937e62a
- https://gist.github.com/sneal/39d47401e9eaefcf8727

## NOTES

- The command `vagrant rdp` may fail, this can be fixed by deleting the line with the faulty fingerprint in `~/.config/freerdp/known-hosts`. 
