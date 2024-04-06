## Description

This project is a MRE to showcase that R8's `-renamesourcefileattribute` option is enabled when R8's full mode is used.

You can see the discussion on [Android Study Group Slack](https://androidstudygroup.slack.com/archives/C6MKCJR8V/p1711987719916089) that led to the [documentation change](https://r8-review.googlesource.com/c/r8/+/90721). More context: [R8 full mode enables -renamesourcefileattribute by default](https://github.com/wzieba/til/blob/22118ebd5559a2096de558a6dde3be0031e33a31/Tools/r8-full-mode-renamesourcefileattribute.md)


## How does it work?

Please see GitHub Actions executions: https://github.com/wzieba/R8FullModeRenamesSources/actions/runs/8510285713/job/23307568895

1. It builds a sample app with R8 full mode
2. Then it builds a sample app without R8 full mode (and without `-renamesourcefileattribute`)
3. Then, both `.apk`s are decoded via `apktool`
4. Their `.smali` files are then compared. The `.apk` with full mode has `.source "SourceFile"` headers, while it did not enabled `-renamesourcefileattribute` configuration. The `.apk` with no full mode has `.smali` as expected: with the file name.

<img width="1061" alt="image" src="https://github.com/wzieba/R8FullModeRenamesSources/assets/5845095/712e3674-8aaf-41e6-b5c9-bb1a1a245695">
