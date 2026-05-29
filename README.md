#IkVideoView

A powerful, gesture-driven Android video player widget with zoom, playback speed control, brightness/volume gestures, and Picture-in-Picture support.

https://img.shields.io/badge/Android-3DDC84?style=flat&logo=android&logoColor=white
https://img.shields.io/badge/minSdk-21-blue
https://img.shields.io/badge/license-MIT-green

Features

· 🎬 Full video playback with MediaPlayer integration
· ✨ Pinch-to-zoom with panning (up to 3x zoom)
· 🔊 Edge gestures for brightness (left edge) and volume (right edge)
· ⏩ Horizontal swipe in bottom 30% of screen for seeking
· 👆 Double-tap gestures:
  · Center: Play/Pause + reset zoom
  · Left edge: Rewind 10s (tap multiple times for 20s, 30s, etc.)
  · Right edge: Forward 10s
· 🎚️ Playback speed control (0.5x - 2.0x)
· 📱 Picture-in-Picture support (Android N+)
· 🔒 Touch lock mode to prevent accidental input
· 🎨 Two scale types: FIT_CENTER and CENTER_CROP
· 📊 Customizable SeekBar with time display

Installation

Step 1: Add the dependency

Copy IkVideoView.java into your project, or add as a module.

Step 2: Add the styleable declaration

Add to your res/values/attrs.xml:

```xml
<declare-styleable name="IkVideoView">
    <attr name="videoUri" format="string" />
    <attr name="autoStart" format="boolean" />
    <attr name="scaleType" format="enum">
        <enum name="fitCenter" value="0" />
        <enum name="centerCrop" value="1" />
    </attr>
    <attr name="showSeekBar" format="boolean" />
</declare-styleable>
```

Usage

Basic XML Layout

```xml
<com.ikechi.studio.view. video.IkVideoView
    android:id="@+id/videoView"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    app:videoUri="android.resource://com.example.app/raw/sample_video"
    app:autoStart="true"
    app:scaleType="fitCenter"
    app:showSeekBar="true" />
```

Programmatic Usage

```java
IkVideoView videoView = findViewById(R.id.videoView);

// Set video source
videoView.setVideoURI(Uri.parse("https://example.com/video.mp4"));

// Control playback
videoView.start();
videoView.pause();
videoView.resume();
videoView.stop();

// Set playback speed (0.5 - 2.0)
videoView.setPlaybackSpeed(1.5f);

// Zoom control
videoView.resetZoom();
int zoomPercent = videoView.getZoomPercent();

// Touch lock (prevent all gestures)
videoView.setTouchLocked(true);

// SeekBar visibility
videoView.setSeekBarVisible(true);
```

Listeners

```java
videoView.setOnPreparedListener(mp -> {
    // Video is ready
});

videoView.setOnCompletionListener(mp -> {
    // Playback finished
});

videoView.setOnErrorListener((mp, what, extra) -> {
    // Handle error
    return true;
});

videoView.setPlaybackStateListener(paused -> {
    // Playback state changed
});

videoView.setSeekbarListener((position, fromUser) -> {
    // Seek position changed
});

videoView.setClickListener(v -> {
    // Single tap detected
});

videoView.setOnPictureInPictureModeChangedListener(isInPip -> {
    // PIP mode changed
});
```

Picture-in-Picture

```java
// Enter PIP mode (Android N+)
if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.N) {
    videoView.enterPictureInPictureMode();
}

// Handle PIP in your Activity
@Override
public void onPictureInPictureModeChanged(boolean isInPip, Configuration newConfig) {
    super.onPictureInPictureModeChanged(isInPip, newConfig);
    if (videoView != null) {
        videoView.dispatchPictureInPictureModeChanged(isInPip);
    }
}
```

Gesture Reference

Gesture Action
Single tap Trigger click listener
Double tap (center) Play/Pause + Reset zoom
Double tap (left 18% edge) Rewind 10s
Double tap (right 18% edge) Forward 10s
Pinch Zoom in/out (0.5x - 3x)
Pan (two-finger after zoom) Move zoomed view
Vertical swipe (left edge) Adjust brightness
Vertical swipe (right edge) Adjust volume
Horizontal swipe (bottom 30%) Seek forward/backward

XML Attributes

Attribute Type Default Description
videoUri string null URI of the video to play
autoStart boolean false Start playing automatically when prepared
scaleType enum fitCenter fitCenter or centerCrop
showSeekBar boolean true Show/hide the SeekBar

Public API

Playback Control

· start() - Start or resume playback
· pause() - Pause playback
· resume() - Resume from paused state
· stop() - Release media player
· seekTo(int msec) - Seek to position
· isPlaying() - Check if playing
· getDuration() - Get video duration (ms)
· getCurrentPosition() - Get current position (ms)
· isCompleted() - Check if playback completed

Speed Control

· setPlaybackSpeed(float speed) - Set speed (0.5 - 2.0)
· getPlaybackSpeed() - Get current speed

Zoom Control

· resetZoom() - Reset to 1x zoom
· getZoomPercent() - Get current zoom percentage

UI

· setSeekBarVisible(boolean visible) - Show/hide SeekBar
· setScaleType(ScaleType type) - Change scale type

Touch Lock

· setTouchLocked(boolean locked) - Lock/unlock all touch gestures
· isTouchLocked() - Check touch lock state

Requirements

· minSdk: 21 (Android 5.0)
· targetSdk: As per your project

Dependencies

None external - uses standard Android framework classes only:

· MediaPlayer
· TextureView
· GestureDetector
· ScaleGestureDetector
· AudioManager

License

MIT License - feel free to use in commercial and personal projects.

Author

Ikechi Studios

---

For issues or feature requests, please open an issue on GitHub.
