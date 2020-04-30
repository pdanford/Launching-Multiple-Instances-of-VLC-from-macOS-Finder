Launching Multiple Instances of VLC from macOS Finder
-----------------------------------------------------

Based on: 
[videolan's wiki](https://wiki.videolan.org/VLC_HowTo/Play_multiple_instances)

The above referenced version does not work with later versions of macOS (e.g. Catalina). The below modified version does.

pdanford - April 2020

---
#### AppleScript Script

Running multiple instances of VLC is not supported out of the box. As a workaround, you can create a AppleScript App that launches separate instances of VLC instead:

1. Run Automator, `File -> New` and choose **Application**.
2. Click `Library -> Utilities` and double click **Run AppleScript**.
3. Paste the script from [AppleScript](#AppleScript) section below.
4. Save; if Automator tries to save to iCloud drive, better to save locally - save as **vlc-m.app** to the Desktop and then move it to **~/Library/Services**.

Set up Finder associations with the vlc-m.app:

1. Open `Finder` and find a video file of interest.
2. Select the file and do <kbd>command</kbd>+<kbd>i</kbd>.
3. Under `Open with:`, click the dropdown and select Other - then navigate to where vlc-m.app is saved and select
4. Click `Change All` button.
5. If prompted "are you sure", select "Yes".
6. Repeat the above for each video file extension type for which you want this active.

Multiple videos can be opened by:
- drop one or more video files onto vlc-m.app
- double click on the selected files in Finder to launch the files in a new standalone VLC sessions
- select multiple video files in Finder and do <kbd>command</kbd>+<kbd>o</kbd>

---
###### AppleScript

    on run {input, parameters}
        tell application "Finder" to set fileList to (get selection as alias list)
        openThese(fileList)
    end run

    on openThese(fileList)
        repeat with theFile in fileList
            do shell script "open -na /Applications/VLC.app " & quote & (POSIX path of theFile) & quote
        end repeat
    end openThese

---
:scroll: [MIT License](README.license)
