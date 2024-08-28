---
icon: box-open
---

# Unpacking the IPA

{% hint style="info" %}
**Good to know:** depending on the product you're building, it can be useful to explicitly document use cases. Got a product that can be used by a bunch of people in different ways? Maybe consider splitting it out!
{% endhint %}

An iOS application IPA file is essentially a ZIP archive, which means it can be unzipped using standard archive utilities available on different operating systems. The process is straightforward and similar to extracting any other ZIP file.

Rename the file extension from .ipa to .zip&#x20;

```bash
mv <app>.ipa <app>.zip
unzip <app>.zip -d App/
```

To decode the executable, and save the data our for post-processing:

First obtain the executable name

/usr/libexec/PlistBuddy -c Print:CFBundleExecutable App/Payload/Example.app/Info.plist

## Dump headers from the executable (use the output of the last command for ${BINARY})

ktool dump --headers --out App/headers App/Payload/Example.app/${BINARY}

## Dump strings from the executable

/usr/bin/strings -n 6 binary > App/Strings.txt

## Dump classes & methods

/usr/bin/otool -oV binary > App/Classes\_Methods.txt\
