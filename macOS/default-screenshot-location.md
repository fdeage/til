# Default Screenshot Location

By default, Mac saves all screenshots to `~/Desktop`.
To save your screenshots in the `~/screenshots` directory:

```bash
$ mkdir ~/screenshots
$ defaults write com.apple.screencapture location ~/screenshots
$ killall SystemUIServer
```

[source](http://osxdaily.com/2011/01/26/change-the-screenshot-save-file-location-in-mac-os-x/)
