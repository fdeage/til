# Cleaning up and saving space in macOS

> Use `du -mhc -d 1` for a quick (non-recursive) space check in a directory


## Basics

- iMovie
- GarageBand


## XCode
[Yop](https://macperformanceguide.com/blog/2016/20161031_1600-XCode-saving-space.html)

Xcode natively takes ~5 GB so...
```
cd /Applications/Xcode.app/Contents/Developer/Platforms/
sudo rm -rf AppleTV* Watch* iPhone*
```

If you don't use Swift:
```
sudo rm -rf /Applications/Xcode.app/Contents/Developer/Toolchains/Swift_2.3.xctoolchain
```

This can save another 3.1 GB (!):
```
rm -rf ~/Library/Developer/Xcode/iOS\ DeviceSupport/*
```

And here is another ~1 GB (this removes support for iPhone/iPad/etc simulators):
```
rm -rf ~/Library/Developer/CoreSimulator/Devices/*
```

## Brew
You may not be aware that every time you upgrade your brew formulas using `brew update && brew upgrade`, Homebrew is leaving behind a copy of the old versions.

`brew cleanup` clears all old versions of brew (can add up to several GB).

Can be used with `-n` or `--dry-run`

## Ruby/gem
`gem cleanup` for xxx (`-n` or `-d` for dry-run)

The cleanup will respect any dependencies on old versions that a gem might have, asking you about each as it goes.

## npm
`npm cache clean [--force]`

## AppStore updates
`$TMPDIR../C/com.apple.appstore/` contains a lot of tmp stuff you might not need, check for yourself (several GB to save there).

Also check `/var/folders/zz` sometimes.

Just **don't delete** `/private/var/db` **since it contains a lot of important stuff (dylibs, system stats, etc.)**

## SleepImage

`private/var/vm/` 
is used to store a copy of your RAM during hibernation.

You can safely remove it and it will just be created again automatically the next time your Mac is put to sleep.

### Disabling sleepimage
Check first which hibernate mode is active:
`pmset -g | grep hibernatemode`

Hibernate modes:

- `hibernatemode = 0` (default on supported desktops). The system will not back memory up to persistent storage. The system must wake from the contents of memory; the system will lose context on power loss. This is, historically, plain old sleep.

- `hibernatemode = 3` (default on supported portables). The system will store a copy of memory to persistent storage (the disk), and will power memory during sleep. The system will wake from memory, unless a power loss forces it to restore from disk image.

- `hibernatemode = 25` is only settable via pmset. The system will store a copy of memory to persistent storage (the disk), and will remove power to memory. The system will restore from disk image. If you want "hibernation" - slower sleeps, slower wakes, and better battery life, you should use this setting.

Choose your mode and set it:
`sudo pmset -a hibernatemode 0`

Then (if you picked `0`):
`sudo rm /private/var/vm/sleepimage`

TIP:
If you only use one account on your mac, you can just point the sleepimage to your `.Trash` folder and empty your trash bin after wake up:
`sudo pmset -a hibernatefile ~/.Trash/sleepimage`

(If for whatever reason you want to return to the factory settings, just type
`sudo pmset -a hibernatefile /var/vm/sleepimage`)



TIP #2:
There's a way to get around sleepimage recreation and therefore permanently free the disk space occupied by sleepimage.

1. disable hibernation mode:
`sudo pmset -a hibernatemode 0`
2. delete `sleepimage`:
`sudo rm /private/var/vm/sleepimage`
3. create an empty file and name it 'sleepimage':
`sudo touch /private/var/vm/sleepimage`
4. change its flag to immutable:
`sudo chflags schg /private/var/vm/sleepimage`


### Swapfiles: `/private/var/vm/swapfile[0-3]`
You can delete them. You can even tell your Mac to never swap again. But you shouldn't. Even on systems that have a lot of memory, your Mac might find a need to swap to its storage space instead of use its primary memory, or RAM.

If you delete your swapfiles, you might cause your system to crash, as it's possible that your Mac is using one of them right as you delete it. The same goes for whether you should disable the ability for your Mac to use swapfiles in the first place - the best result is that you won't notice a difference, and it's more likely to make your Mac increasingly unstable.

If you really need to free up some space taken up by your Mac's swapfiles, there's an easy and simple fix: just reboot your Mac. Shut it down and restart it, and then check your swapfile directory again - they should either be gone or substantially reduced in size.


## Back-ups
In iTunes, `Preferences > Devices > backups` will show you all the backups of external devices that iTunes might have (silently) done.

## Docker
Try emptying the images in ```~/Library/Containers/com.docker.docker/```


## Caches

### Chrome

- `~/Library/Application Support/Google/Chrome`
- `~/Library/Caches/Google/Chrome/Default`
- `~/Library/Caches/com.google.Chrome`
- `~/Library/Caches/com.google.Keystone.Agent`
- `~/Library/Caches/com.google.SoftwareUpdate`
- `~/Library/Caches/com.googlecode.iterm2`
- `~/Library/Google`

### Other spots to check

- /System/Library/LaunchDaemons/[Application]
- /System/Library/LaunchAgents/[Application]
- /Applications/[Application]
- ~/Applications/[Application]
- ~/Library/Application Support/[Application]
- ~/Library/Preferences/[Application]
- ~/Library/Caches/[Application]
- ~/Library/Containers/Application]
- ~/Library/LaunchAgents/Application]
- ~/Library/PreferencePanes/[Application]
- ~/Library/Saved\ Application\ State/[Application]
