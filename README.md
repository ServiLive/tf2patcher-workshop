# TF2 patcher for increased Workshop upload limit

## Summary

This tool raises the 200 MiB (209.7 MB) workshop map upload limit in TF2.

This is a fork of [tf2patcher by yari-dog](https://github.com/yari-dog/tf2patcher-linux) only changed to patch and increase the map upload limit in-game (take in mind that from my tests, the max workshop map file size a map can be is something around 900 MB (also keep in mind that you need to have enough space in the TF2 Steam Cloud)).

Bigger map sizes may take more than 10 minutes to upload (tested with [buzzies_dream_box_v1](https://steamcommunity.com/sharedfiles/filedetails/?id=3839085225) by [Chromsmith](https://steamcommunity.com/id/chromsmith)).

## Is it safe?

> [!CAUTION]  
> **USE AT YOUR OWN RISK.**
>
> This tool could be detected by VAC. **However:**
>
> - I recommend running TF2 in ``-insecure`` mode while you do this.
> - If running this tool without ``-insecure``, **make sure to close TF2 before connecting to Casual or community servers**. You can then safely open it again. This is not strictly
    necessary, but it's best to clear all memory modifications before connecting to a secure server.

## How to use

### Windows

1. Download the latest release [here](https://github.com/ServiLive/tf2patcher-workshop/releases/latest);

2. Run tf2patcher and launch TF2 (or do it in reverse, the order does not matter. Linux shouldn't require sudo/doas);

3. Now try uploading or updating a map to the workshop (big map filesize may take a lot of time);

4. **After you finished with the tool, close TF2 in order to remove any modifications caused by the patcher.**

### Building Windows

Requires MinGW-w64 (`gcc`, `make` and `windres`). Run `make TARGET=64`.

### Building Linux

Requires `gcc` and `make`. Run `make TARGET=64`.

## How does it work

What exactly gets patched:

- The `unFileSize > kMaxFileSize` check in [`CTFFileUGCUploadHandler::OnFilePrepared`](https://github.com/ValveSoftware/source-sdk-2013/blob/3e957b70b167929f120360115d359d1ecb4c1699/src/game/client/tf/workshop/published_files.cpp#L389) gets its constant changed from 200 MiB to 4 GiB, raising the client-side size upload limit. Empty (0 byte) files are still rejected, and Steam's own Workshop size limit still applies (860 MiB approximately or 900 MB).

## License

See UNLICENSE file.
