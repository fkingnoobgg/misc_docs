# misc_docs

## Electron
In my experience, the biggest cause of slow app startup is having too many require() calls at the top of your main.js.

By design, require() is synchronous. And it can touch lots of files on the filesystem. If your users have a spinning disk drive, then all the random accesses will kill your startup time. You can improve the situation by bundling your app with ASAR, so only one file needs to be read.

Another huge win is to optimize the order that you require() files. By lazy loading as much as possible, we were able to get WebTorrent Desktop to under 500ms startup time on a Macbook 12" (basically a netbook with an SSD).

It is possible to build fast apps with Electron, but you have to be ruthless about lazy loading, and choosing small, focused modules over huge framework modules. I think of it as similar to developing for mobile -- you want to parse as little JavaScript as possible before your app window shows up.
[Source](https://github.com/electron/electron/issues/5672#issuecomment-222053637)
