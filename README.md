Opening multiple instances of VLC
---------------------------------

Based on: 
[https://wiki.videolan.org/VLC_HowTo/Play_multiple_instances](https://wiki.videolan.org/VLC_HowTo/Play_multiple_instances)

pdanford - April 2020

---
#### App Script

Running multiple instances of VLC is not supported out of the box.

As a workaround, you can create a Droplet/App that does the following:
- launch the VLC droplet/app to get a separate instance of VLC
- drop one or more files onto VLC droplet/app
- or associate your .mov, .avi, and other files directly with the VLC droplet/app, allowing you to simply click on the files to launch the files in a new standalone VLC session.

Paste the code below into a new AppleScript Editor script and save it as an application.

    on run
        do shell script "open -n /Applications/VLC.app"
        tell application "VLC" to activate
    end run

    on open theFiles
        repeat with theFile in theFiles
            do shell script "open -na /Applications/VLC.app " & quote & (POSIX path of theFile) & quote
        end repeat
        tell application "VLC" to activate
    end open

File Association with the Droplet/App can be done as follows:

1. Open `Finder` and find the video file of interest
2. Right click on the file (assumes you have right click enabled)
3. Choose `Get Info`
4. Under `Open with:`, click dropdown and select the VLC droplet/app
5. Click `Change All` button
6. If prompted "are you sure", select "Yes".

---
#### Command-line

Use the option --no-one-instance.

On \*nix systems you can create background jobs:

    vlc --no-one-instance file1.ogg & vlc --no-one-instance file2.ogg

On Windows systems you might use START:

    START "VLC media player - Instance 1" "%PROGRAMFILES%\VideoLAN\VLC\vlc.exe" "--no-one-instance file1.ogg" && START "VLC media player - Instance 2" "%PROGRAMFILES%\VideoLAN\VLC\vlc.exe" "--no-one-instance file2.ogg"
