# Working with AVFoundation - Recording & Saving Videos

### Objectives

- Record and save assets(video, audio, images) with AVFoundation
- Exporting assets


## AVAsset

AVAsset reepresents timed audiovisual media such as video and audio which contain a collection of tracks that are intended to be processed as a unit.

## AVComposition

An AVComposition is a collection of tracks, each presenting media of a specific type such as audio or video, according to a timeline. Each track is represented by an instance of AVCompositionTrack.

## AVMutableComposition

Contains instances of AVMutableCompositionTrack. 

## AVMutableCompositionTrack

AVMutableCompositionTracks represent an asset to be played.


## AVAssetExportSession


## Steps

1. Create an AVMutableComposition object to hold your video and audio tracks and transform effects.