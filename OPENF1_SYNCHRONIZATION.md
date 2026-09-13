# OpenF1 video-clock synchronization

Singapore 2024 Norris qualifying uses an approximate lap-start video offset of 1.6 seconds: inspected video times 60 and 80 seconds show lap-clock values 58.4 and 78.4 seconds. Spain 2024 uses 5.2 seconds: video times 50 and 70 show 44.8 and 64.8 seconds. Broadcast clocks round to tenths; frozen sector graphics were excluded from alignment anchors.

These anchors are saved with the downloaded showcase data. The circuit panel maps playback time to the lap UTC start and selects the nearest telemetry/location sample within 750 milliseconds. No sample is returned outside the lap or when the asset/session does not match. A moving point represents approximate recorded location on the side map. An explicit manual timing control can save annotations for other footage.

Three synchronization tests pass, including mismatched footage and absent samples. The production build passes. Browser verification at Singapore video time 60 seconds showed synchronized telemetry, including 137 km/h and gear 3. No backend restart was performed; current processing continues.

OpenF1 supplies telemetry and location traces, not legal boundary polygons or 3D circuit models. This change synchronizes the reference panel, not a camera-space track boundary. It does not solve false white-object detections. Camera registration with suitable track-edge geometry and independently evaluated perception remain outstanding. Edited highlights require segment-specific matching rather than one global offset.

Source: https://openf1.org/docs/
