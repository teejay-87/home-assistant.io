---
layout: page
title: "Image Processing"
description: "Instructions on how to setup image processing with Home Assistant."
date: 2017-01-09 00:00
sidebar: true
comments: false
sharing: true
footer: true
ha_release: 0.36
---

Image processing enables Home Assistant to process images from [cameras](/components/#camera). Only camera entities are supported as sources.

For interval control, use `scan_interval` in platform.

<p class='note'>
If you are running Home Assistant over SSL or from within a container, you will have to setup a base URL (`base_url`) inside the [http component](/components/http/).
</p>

## {% linkable_title ALPR %}

ALPR entities have a vehicle counter attribute `vehicles` and all found plates are stored in the `plates` attribute.

The `found_plate` event is triggered after OpenALPR has found a new license plate.

```yaml
# Example configuration.yaml automation entry
automation:
- alias: Open garage door
  trigger:
    platform: event
    event_type: image_processing.found_plate
    event_data:
      entity_id: openalpr.camera_garage_1
      plate: BE2183423
...
```

The following event attributes will be present (platform-dependent): `entity_id`, `plate`, `confidence`

## {% linkable_title Face %}

Face entities have a face counter attribute `total_faces` and all face data is stored in the `faces` attribute.

The `detect_face` event is triggered after a Face entity has found a face.

```yaml
# Example configuration.yaml automation entry
automation:
- alias: Known person in front of my door
  trigger:
    platform: event
    event_type: image_processing.detect_face
    event_data:
      entity_id: image_processing.door
      name: 'Hans Maier'
...
```

The following event attributes will be present (platform-dependent): `entity_id`, `name`, `confidence`, `age`, `gender`, `motion`, `glasses`
