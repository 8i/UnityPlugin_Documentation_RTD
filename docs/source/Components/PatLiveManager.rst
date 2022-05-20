PatLiveManager
============================================================

| This component helps to connect a PatActor to Asgard live streams.
| NOTE: You must have your own Asgard live stream URL. As testing requires a live stage to operate, there is no sample URL provided.
| It takes in the Asgard live URL and monitors whether the stream is active or not.
| When the stream becomes active, it will pull the current live MPD URL, assign it to the PatActor, and begin playing.
| The manager does not stop playback when the stream becomes inactive. Since there is a delay between playback and the stream, this allows any remaining stream data to finish playing.
| The Manager has a callback for when the stream status changes.

Parameters
------------------------------------------------------------

- AsgardLiveShowUrl: The URL to monitor for live stream status changes
- CheckStatePeriod: How often to check the URL when the stream is inactive
- onStreamActiveChanged: Callback invoked when the stream status changes
- Active: Enable to allow the Manager to make network requests and begin playback as needed.
