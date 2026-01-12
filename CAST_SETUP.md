# Google Chromecast Streaming Setup Guide

## Overview
The StreamFlow video player now includes full Google Chromecast streaming functionality, allowing you to stream videos from your browser directly to Chromecast devices.

## Features

### ✅ What's Included
- **Device Discovery**: Automatically finds available Chromecast devices on your network
- **One-Click Casting**: Simple casting with a single button click
- **Playback Control**: Control playback (play/pause) on both local and remote devices
- **Status Indicator**: Visual feedback showing casting status
- **Automatic Sync**: Syncs current playback position when casting
- **Format Support**: Works with MP4, WebM, HLS (m3u8), and DASH (mpd) streams
- **Metadata**: Shows video title and URL on Cast device display

## Requirements

### Browser Support
- **Chrome/Chromium**: Full support (recommended)
- **Edge**: Full support
- **Firefox**: Requires Cast extension
- **Safari**: Limited support

### Hardware
- Chromecast device (1st gen or newer)
- Google Home/Nest Hub
- Sony TV with Chromecast built-in
- Or any device with Chromecast support

### Network
- Same WiFi network as Chromecast device
- Stable internet connection (minimum 2 Mbps for HD video)

## Setup Instructions

### 1. Enable Google Cast in Your Browser

#### Chrome
1. Open Chrome and go to settings
2. Look for "Experimental features" or "About Chrome"
3. Ensure Google Cast is enabled (usually enabled by default)
4. Restart Chrome

#### Edge
1. Open Edge settings
2. Go to Privacy, search and services
3. Ensure media playback is enabled

### 2. Connect to WiFi Network
- Ensure your computer and Chromecast device are on the same WiFi network
- Power on your Chromecast device

### 3. Test Cast Functionality

1. **Open the StreamFlow player**
   ```
   http://localhost:4000
   ```

2. **Load a video**
   - Paste a direct video URL (MP4, WebM, etc.)
   - Or select a HLS/DASH stream
   - Click "Stream"

3. **Locate the Cast Button**
   - In the video player controls (bottom right)
   - Look for the Cast icon (looks like a TV with WiFi symbol)

4. **Click to Cast**
   - Click the Cast button
   - Select your Chromecast device from the list
   - Video will start playing on your TV

## Usage Guide

### Basic Casting

1. **Load Video**
   ```
   Enter video URL → Click Stream
   ```

2. **Open Cast Menu**
   ```
   Click Cast icon in controls
   ```

3. **Select Device**
   ```
   Choose from available Chromecast devices
   ```

4. **Video Starts Playing**
   ```
   On your TV in seconds
   ```

### Playback Control

While casting, you can:
- **Play/Pause**: Space bar or play button (controls TV playback)
- **Seek**: Click progress bar (seeks on remote)
- **Volume**: Keyboard arrows (controls TV volume)
- **Stop Casting**: Click back button to return to local playback

### Keyboard Shortcuts While Casting
- `Space` - Play/Pause on TV
- `→` - Skip 10s (on TV)
- `←` - Back 10s (on TV)
- `↑/↓` - Volume control
- `F` - Can still use fullscreen (shows on TV)

## Supported Video Formats

| Format | Support | Notes |
|--------|---------|-------|
| MP4 | ✅ Full | Most compatible |
| WebM | ✅ Full | VP8/VP9 codec |
| OGG | ✅ Full | Theora codec |
| HLS (.m3u8) | ✅ Full | Adaptive bitrate |
| DASH (.mpd) | ✅ Full | Adaptive bitrate |

## Troubleshooting

### Device Not Appearing in Cast Menu

**Problem**: "No Cast devices available" message

**Solutions**:
1. ✅ Restart your Chromecast device (unplug for 10 seconds)
2. ✅ Restart your browser
3. ✅ Verify both devices are on same WiFi
4. ✅ Check if Cast is enabled in browser settings
5. ✅ Try opening a different website and cast from there

### "Cannot Play This Video" on TV

**Problem**: Video starts playing but shows error on TV

**Solutions**:
1. Check if video format is supported (MP4/WebM are most compatible)
2. Try using the proxy option if video is blocked
3. Verify video URL is publicly accessible
4. Check browser console for error messages

### Casting Starts Then Stops

**Problem**: Video plays for a few seconds then stops

**Solutions**:
1. Check internet connection stability
2. Try reducing video quality/bitrate
3. Ensure local firewall isn't blocking Chromecast protocol
4. Check if video URL has expiration time

### Controls Don't Respond

**Problem**: Play/Pause buttons don't work while casting

**Solutions**:
1. Disconnect and reconnect Cast session
2. Refresh the player page
3. Check if browser has focus (click on player)
4. Try controlling from Chromecast remote

### Video Format Error

**Problem**: "Video format not supported by browser"

**Solutions**:
1. Use MP4 format (most universal)
2. Try converting video to supported format
3. Check if Chromecast device supports the codec
4. For HLS, ensure `.m3u8` extension is correct

## Advanced Configuration

### Custom Receiver App

To use a custom Cast receiver app:

```javascript
castContext.setOptions({
    receiverApplicationId: 'YOUR_CUSTOM_APP_ID',
    autoJoinPolicy: chrome.cast.AutoJoinPolicy.ORIGIN_SCOPED
});
```

### Bitrate Optimization

For slower connections, use HLS/DASH streams which adapt to your bandwidth:
```
https://example.com/video.m3u8  (HLS)
https://example.com/video.mpd   (DASH)
```

## Security & Privacy

- ✅ Casting works on secure (HTTPS) connections
- ✅ Your video URL is sent to Chromecast device for playback
- ✅ No data is stored on the server
- ✅ Proxy option available for blocked content

## Performance Tips

### For Best Casting Experience:

1. **Use Wired Network**: If possible, connect Chromecast with Ethernet
2. **Reduce Interference**: Keep WiFi router close to Chromecast
3. **Quality Settings**: 
   - HD content (5 Mbps): Recommended for stable streaming
   - 4K content (15+ Mbps): Requires strong WiFi signal
4. **Buffer Management**: Player automatically buffers ahead
5. **Video Optimization**: 
   - MP4 with H.264 codec (most compatible)
   - AAC audio codec

## FAQ

### Q: Can I cast from my phone?
**A**: Yes, through mobile Chrome browser. YouTube and other apps also support casting.

### Q: What if my video URL expires?
**A**: Get a fresh URL. Google Drive links expire after a few hours.

### Q: Can I cast to multiple devices?
**A**: Only one Chromecast device per browser session.

### Q: Does casting work offline?
**A**: No, you need internet to stream content to your TV.

### Q: Can I use a VPN while casting?
**A**: Your Chromecast device must be on the same network, so VPN may not work. Disable VPN or use split tunneling.

### Q: Why is there a delay between clicking and playback?
**A**: Network latency. This is normal (usually 1-3 seconds).

## Technical Details

### How It Works
1. Player detects available Chromecast devices
2. User selects device from menu
3. Player sends video URL and metadata to Chromecast
4. Chromecast device streams video directly from source
5. Browser controls remote playback via Cast protocol

### API Used
- **Chrome Cast SDK**: `chrome.cast` API v2
- **Default Receiver App**: Standard Media Receiver
- **Protocol**: DIAL (Discovery and Launch)

## Getting Help

If you encounter issues:

1. **Check Browser Console** (F12 → Console tab)
   - Look for error messages starting with "Cast" or "🎬"

2. **Review Network Tab** (F12 → Network tab)
   - Verify video URL loads successfully
   - Check for CORS errors

3. **Device Status**
   - Power cycle Chromecast
   - Check WiFi connection
   - Verify device firmware is updated

## Future Enhancements

Planned features:
- [ ] Receive from Chromecast (display Cast device screen)
- [ ] Queue management (multiple videos)
- [ ] Subtitle support during casting
- [ ] Audio track selection
- [ ] Wireless screen mirroring

## Support Resources

- **Google Cast Documentation**: https://developers.google.com/cast
- **Chromecast Troubleshooting**: https://support.google.com/chromecast
- **WebRTC Standards**: https://webrtc.org/

---

**Version**: 1.0.0  
**Last Updated**: January 2026  
**Compatibility**: Chrome 50+, Edge 79+, Firefox (with extension)
