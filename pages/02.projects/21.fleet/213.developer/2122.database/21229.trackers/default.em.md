# Tracker and TrackerHeartBeatData Models Documentation

This document provides an overview of the `Tracker` and `TrackerHeartBeatData` models within the Prisma schema, including their relationships and fields.

## Model: Tracker

### Fields

- `id`: An integer that serves as the unique identifier for each `Tracker` record. It is auto-incremented.
- `name`: A string representing the name of the tracker.
- `vehicleId`: An optional integer that stores the ID of the associated vehicle. This field is unique, meaning each tracker can be associated with at most one vehicle.
- `vehicle`: A relation field that links to the `Vehicle` model. This field represents the vehicle associated with the tracker. If the associated vehicle is deleted, the `vehicleId` in the `Tracker` model is set to null due to the `onDelete: SetNull` action.
- `heartBeats`: A relation field that links to the `TrackerHeartBeatData` model. This field represents the heartbeat data associated with the tracker.

### Relations

- `vehicle`: This model has a one-to-one relation with the `Vehicle` model. Each `Tracker` can be associated with one `Vehicle`, and each `Vehicle` can have one `Tracker`.
- `heartBeats`: This model has a one-to-many relation with the `TrackerHeartBeatData` model. Each `Tracker` can have multiple `TrackerHeartBeatData` records.

## Model: TrackerHeartBeatData

### Fields

- `id`: An integer that serves as the unique identifier for each `TrackerHeartBeatData` record. It is auto-incremented.
- `timeStamp`: A DateTime field that stores the timestamp of the heartbeat. It defaults to the current date and time.
- `latitude`: A float representing the latitude of the heartbeat.
- `longitude`: A float representing the longitude of the heartbeat.
- `trackerId`: An integer that stores the ID of the associated tracker.
- `tracker`: A relation field that links to the `Tracker` model. This field represents the tracker associated with the heartbeat data.

### Relations

- `tracker`: This model has a one-to-many relation with the `Tracker` model. Each `TrackerHeartBeatData` is associated with one `Tracker`, and each `Tracker` can have multiple `TrackerHeartBeatData` records.