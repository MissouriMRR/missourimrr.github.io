# Importing from Skybrush

To import from Skybrush, you export a folder of CSVs.
These CSVs contain the location of the drones at any given point in
the sequence. These csvs should be moved, along with keyframe and rotation
CSVs, to "Lightshow install location"/models/Skybrush_CSV.

The primary exported CSVs can be converted into LLA CSVs with the help of
the keyframe and rotation CSVs. The script to do this is install_location/choreography/csv_lla_converter.py

```
uv run csv_lla_converter.py
```

Afterwords, update the configuration for the lightshow by running

```
uv run lla_to_config.py
```

In the same folder.
