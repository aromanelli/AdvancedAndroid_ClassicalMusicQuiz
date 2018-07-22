[From Lession 6, Media Playback](https://classroom.udacity.com/nanodegrees/nd801/parts/443745fb-4ae4-4918-8ea1-6bf24e356c1d/modules/6cb81da9-d083-4721-a31b-4f435de9fedd/lessons/89b6a627-f121-498c-aa53-26304544b5f3/concepts/c6a354c3-217d-439f-a298-4f1840211796)

# Android Media Framework Extras

## Audio Focus

This is how the Android framework knows about different applications using audio. If you want your app to fade out when other important notifications (such as navigation) occur, you'll need to learn how your app can "hop in line" to be the one in charge of audio playback, until another app requests focus.

## Noisy Intent

There are certain conditions that you will want to check for. For example, imagine you are blasting your favorite song at full volume. Little does anyone know, but your favorite song is "Itsy Bitsy Spider". Right when it's about to get to the best part, you trip and yank out the headphones from the audio port. Suddenly the whole world knows your secret. Not the best experience right? Luckily the android framework sends out the [ACTION_AUDIO_BECOMING_NOISY](https://developer.android.com/reference/android/media/AudioManager.html#ACTION_AUDIO_BECOMING_NOISY) intent when this occurs. This allows you to register a broadcast receiver and take a specific action when this occurs (like pausing the music and saving yourself of embarrassment).

## Audio Stream

Android uses separate audio streams for playing music, alarms, notifications, the incoming call ringer, system sounds, in-call volume, and DTMF tones. This allows users to control the volume of each stream independently.

By default, pressing the volume control modifies the volume of the active audio stream. If your app isn't currently playing anything, hitting the volume keys adjusts the ringer volume. To ensure that volume controls adjust the correct stream, you should call [setVolumeControlStream()](https://developer.android.com/reference/android/app/Activity.html#setVolumeControlStream(int)) passing in [AudioManager.STREAM_MUSIC](https://developer.android.com/reference/android/media/AudioManager.html#STREAM_MUSIC).

# ExoPlayer Extras

## Subtitle Side Loading

Given a video file and a separate subtitle file, MergingMediaSource can be used to merge them into a single source for playback.

```
MediaSource videoSource = new ExtractorMediaSource(videoUri, ...);
MediaSource subtitleSource = new SingleSampleMediaSource(subtitleUri, ...);
// Plays the video with the sideloaded subtitle.
MergingMediaSource mergedSource =
    new MergingMediaSource(videoSource, subtitleSource);
```
## Looping a video

A video can be seamlessly looped using a LoopingMediaSource. The following example loops a video indefinitely. It’s also possible to specify a finite loop count when creating a LoopingMediaSource.

```
MediaSource source = new ExtractorMediaSource(videoUri, ...);
// Loops the video indefinitely.
LoopingMediaSource loopingSource = new LoopingMediaSource(source);
```