# Codrut's Windows Runtime for Delphi -> Media Controls
Media Playback Controls Delphi integration for Windows 8/8.1/10/11

## Source and Dependencies
This library is part of the [Codrut's Windows Runtime for Delphi](https://github.com/Codrax/Cod-Windows-Runtime), all units can be found there.

Attention! The app must be registered with a TAppRegistration, for futher detalies, look at the Cod Windows Runtime docs.

## Examples
### Creating the Transport controls
```
  PlayControls := TWindowMediaTransportControls.Create;
```
### Setting media type and supported media controls
```
  PlayControls.MediaPlaybackType := TMediaPlaybackType.Music;
  PlayControls.SupportedMediaControls := [TMediaControlAction.Play,
    TMediaControlAction.Pause, TMediaControlAction.Stop,
    TMediaControlAction.SkipPrevious, TMediaControlAction.SkipNext];
```
### Setting media information
```
  // Set info (in this case music, but for other types use the respective class)
  PlayControls.InfoMusic.Title := 'Song name';
  PlayControls.InfoMusic.AlbumArtist := 'Artist123';

  // PlayControls.Thumbnail := ImageGraphic; // a PNG, JPEG, GIF or valid image type supported by windows

  PlayControls.UpdateInformation;
```
### Enabling the player to display
```
  // Enable
  PlayControls.EnablePlayer := true;
```
### Setting play status
```
  // Status
  PlayControls.PlaybackStatus := TMediaPlaybackStatus.Playing;
```
### Pushing timeline information
For windows, this information is mostly unused as It's not displayed in the Action Center. It's reccomended to not update this too often. Once every few seconds should be enough
```
  // Timeline
  PlayControls.Timeline.StartTime := 0;
  PlayControls.Timeline.EndTime := 90*1000;
  PlayControls.Timeline.Position := 5000;

  PlayControls.PushTimeline;
```
### Registering events
With the help of TSubscriptionEventHandler class, you can register multiple events at the same time.
```
interface
type
  TMyCustomClass = class(TObject)
  public
    procedure RequestPos(Sender: TTransportCompatibleClass; P: int64);
    procedure RequestRate(Sender: TTransportCompatibleClass; R: double);
    procedure RequestShuffle(Sender: TTransportCompatibleClass; S: boolean);
    procedure RequestRepeat(Sender: TTransportCompatibleClass; R: TMediaPlaybackAutoRepeatMode);
  end;

implementation

initialization
  // Events
  PlayControls.OnButtonPressed.Add( ButtonPressed );
  PlayControls.OnPlaybackPositionChangeRequested.Add( RequestPos );
  PlayControls.OnPlaybackRateChangeRequested.Add( RequestRate );
  PlayControls.OnShuffleEnabledChangeRequested.Add( RequestShuffle );
  PlayControls.OnRepeatModeChangeRequested.Add( RequestRepeat );
```

## Pictures
![383184980-cb3d4cae-f037-406a-878a-ffee8be6c135](https://github.com/user-attachments/assets/1a4c070e-1774-4644-b705-6dc9b88ca0f5)
