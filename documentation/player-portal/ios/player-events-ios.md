---
layout: page
title: Player Events for iOS
weight: 110
---

The player and some of the plugins fire events that tell the application (and other plugins) about events that occur before/during/after playback. 

### Listening to events from application code

The code below will add an observer to a list of various events. 

>Reminder to use `weak self` when needed in order to prevent retain cycles

{% highlight swift %}
player.addObserver(self, events: [PlayerEvent.playing, PlayerEvent.durationChanged, PlayerEvent.stateChanged]) { [weak self] event in
    guard let self = self else { return }
    switch event {
    case is PlayerEvent.Playing:
        // handle playing event
        break
    case is PlayerEvent.DurationChanged:
        if let playerEvent = event as? PlayerEvent, let duration = playerEvent.duration as? TimeInterval {
            let duration = duration
        }
    case is PlayerEvent.PlayheadUpdate:
        if let playerEvent = event as? PlayerEvent, let currentTime = playerEvent.currentTime {
            self.playheadSlider.value = Float(self.player.currentTime / self.player.duration)
        }
    case is PlayerEvent.StateChanged:
        let newState = event.newState
        let oldState = event.oldState
    default:
        break
    }
}
{% endhighlight %}

### Listening to events from plugin code

Plugins can't call `addObserver` on the player; instead, an identical function exists on the `MessageBus` object that is passed to the plugin.

## Core Player Events

The Player events are defined in the PlayerEvent class.

### Normal Flow
- **SourceSelected:** Sent when a playback source is selected.
- **LoadedMetadata:** The media's metadata has finished loading, all attributes now contain as much useful information as they're going to.
- **DurationChanged:** The metadata has loaded or changed, indicating a change in duration of the media. This is sent, for example, when the media has loaded enough that the duration is known.
- **TracksAvailable:** Sent when track info is available.
- **PlaybackInfo:** Sent to notify about changes in the playback parameters. When bitrate of the video or audio track changes or new media is loaded. Holds the PlaybackInfo.java object with relevant data.
- **CanPlay:** Sent when enough data is available that the media can be played, at least for a couple of frames. This corresponds to the HAVE_ENOUGH_DATA readyState.
- **Play:** Sent when playback of the media starts after having been paused; that is, when playback is resumed after a prior pause event.
- **Playing:** Sent when the media begins to play (either for the first time, after having been paused, or after ending and then restarting).
- **Ended:** Sent when playback completes.

### Additional User Actions
- **Pause:** Sent when playback is paused.
- **Seeked:** Sent when a seek operation completes.
- **Seeking:** Sent when a seek operation begins.
- **Stopped:** Sent when stop player API is called
- **Replay:** Sent when a replay operation is performed.

### Playhead
- **PlayheadUpdate:** Sent when the playhead (current time) has moved.
- **LoadedTimeRanges:** Sent when loaded time ranges was changed, loaded time ranges represent the buffered content. Could be used to show amount buffered on the playhead UI.

### Track Change
- **VideoTrackChanged:** A video track was selected
- **AudioTrackChanged:** An audio track was selected
- **TextTrackChanged:** A text track was selected

### Metadata (ID3 tags and related)
- **TimedMetadata:** Sent when there is metadata available for this entry.

### State Change
- **StateChanged:** Sent when player state is changed.

The Player can be in one of 4 playback states:

  `idle`, `buffering`, `ready`, `ended`, `error`
  
### Stalled
- **PlaybackStalled:** Sent when the player has stalled. Buffering with no available data to play.

### Errors
- **Error:** Sent when an error occurs. The element's error attribute contains more information. See Error handling for details.
- **ErrorLog:** Sent when an error log event received from player (non fatal errors).


## Ad Events

Defined in AdEvent class.

- streamLoaded // Only in DAI
- streamStarted // Only in DAI
- adBreakReady
- adBreakStarted // Only in DAI
- adBreakEnded // Only in DAI
- adPeriodStarted // Only in DAI
- adPeriodEnded // Only in DAI
- allAdsCompleted
- adComplete
- adClicked
- adFirstQuartile
- adLoaded
- adLog
- adMidpoint
- adPaused
- adResumed
- adSkipped
- adStarted
- adTapped
- adThirdQuartile
- adDidProgressToTime
- adDidRequestContentPause
- adDidRequestContentResume
- adWebOpenerWillOpenExternalBrowser
- adWebOpenerWillOpenInAppBrowser
- adWebOpenerDidOpenInAppBrowser
- adWebOpenerWillCloseInAppBrowser
- adWebOpenerDidCloseInAppBrowser
- adCuePointsUpdate
- adStartedBuffering
- adPlaybackReady
- requestTimedOut
- adsRequested
- error

## Code Sample
- [Events Registration](https://github.com/kaltura/playkit-ios-samples/tree/develop/EventsRegistration)
