---
layout: post
title: Clean My Mac and Free Up Storage
image: https://github.com/vinkla.png
---

There's so much you could clean on your Mac to save space. After a couple months with your new Mac, macOS has been building up a big library of logs, backups and other cached data that necessarily isn't important to save.

Below are commands listed which with you can run in order to free up storage and speedup your computer. Following these easy steps gave me back 10 GB of storage. Lets fire up the Terminal application and lets go.

## Trash

Emptying the Trash could be painful and take a quite some time to finish, if you haven't done it in a while. This is because your Mac has to index the entire Trash directory while deleting files. Don't worry, there is a better way.

The command below isn't only faster than the normal Empty Trash action, it also empties the Trash on all mounted volumes as well as the main drive.

```bash
sudo rm -rfv /Volumes/*/.Trashes
sudo rm -rfv ~/.Trash
```

## System Logs

Apple keeps track of what you're doing by creating log files. These Apple System Logs files slows down your Mac, specially during startup. Remember macOS saves these while you're using your computer. Try to run this command as often as you're emptying the trash.

```bash
sudo rm -rfv /private/var/log/asl/*.asl
sudo rm -rfv /Library/Logs/DiagnosticReports/*
```

## iOS Applications

Have you every connected an iOS device to your Mac? If so, iTunes has probably kept a copy of your iOS applications. You don't need those to be saved on your Mac. Remove them all.

```bash
rm -rfv ~/Music/iTunes/iTunes\ Media/Mobile\ Applications/*
```

> Please note that this will remove all backed-up iOS application on your computer. If you're not sure about what you're doing then please be cautious.

## iOS Software Updates

Whenever you update your iOS device trought iTunes it downloads that entire update locally on your computer. Once you've updated you don't need them anymore.

```bash
rm -rfv ~/Library/iTunes/iPhone\ Software\ Updates/*
```

## Device Backups

With iTunes you can backup your iOS devices to your computer. If you're like me, everything should be stored in iCloud. Then you can remove the backups saved on your system.

```bash
rm -rfv ~/Library/Application\ Support/MobileSync/Backup/*
```

> Please note that this will remove all your iOS system backups on your computer. If you're not sure about what you're doing then please be cautious.

## Xcode Derived Data & Archives

Working with Xcode? If so, Xcode save a lot of derived data. This data is possible to remove via Xcode's interface. Though, I like to remove it from the command-line. Xcode also saves all old archives which you probably don't need anymore.

```bash
# Derived Data
rm -rfv ~/Library/Developer/Xcode/DerivedData/*

# Archives
rm -rfv ~/Library/Developer/Xcode/Archives/*
```

## Homebrew Cache

If you're using [Homebrew](http://brew.sh/) to manage binary packages on your Mac. You could free up storage by deleting the content of its caches directory.

```bash
brew cleanup --force -s
rm -rfv /Library/Caches/Homebrew/*
```

## Wrapping Up

I usually don't run all these commands separately. Instead, I've created a Bash script that cleans up everything at the same time. If you're interested, you can [check it out on GitHub](https://github.com/vinkla/dotfiles/blob/master/bin/cleanup).

If you know of any other junk that is saved in the macOS system. Don't hesitate to add it to the [send me a tweet](https://twitter.com/{{ site.author.twitter }}). If it is good, I'll add it to the article.
