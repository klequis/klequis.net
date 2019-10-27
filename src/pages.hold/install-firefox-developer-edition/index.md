---
title: Install Firefox Developer Edition on Ubuntu 19.04
date: '2019-05-01'
spoiler: Don't know yet
---



[Firefox Developer Edition](https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Developer_Edition) has:
- the latest firefox features
- a separate developer profile
- experimental developer tools
- preferences tailored for web developers
- a distinct theme

> Some advise remove the regular edition of FireFox to avoid conflicts. However, I have been using it side-by-side with the developer edition for a couple of years now without problem.

To install Firefox Developer Edition on Ubuntu 19.04

## Download & Extract
- Go to [Firefox Developer Edition](https://www.mozilla.org/en-US/firefox/developer/) and download Firefox Developer Edition
- Go to the location you downloaded to (likely ~/Downloads)
- Right-click and choose Extract Here
- Open the folder created by extracting

## Move Firefox to /opt
When you extract Firefox Developer Edition you will get a folder something like `firefox-67.0b15' cd into that folder.
```
$ cd firefox-67.0b15
```

## Move /firefox to /opt/firefox-developer
```
$ mkdir -p /opt/firefox-developer
$ sudo mv firefox /opt/firefox-developer
```

## Make a Desktop Icon
- Open a new document in your text editor and enter the following
```
[Desktop Entry]
Name=Firefox Developer
GenericName=Firefox Developer Edition
Exec=/opt/firefox-developer/firefox/firefox
Terminal=false
Icon=/opt/firefox-developer/firefox/browser/chrome/icons/default/default128.png
Type=Application
Categories=Application;Network;X-Developer;
Comment=Firefox Developer Edition Web Browser.
```

- Save the file as 'firefox-developer.desktop'
- Make the file executable
```js
sudo chmod +x firefox-developer.desktop
```
- Move it to /usr/share/application
```js
sudo mv firefox-developer.desktop /usr/share/applications
```

You should now be able launch FireFox Developer Edition!
