---
layout: post
title: "CitiBike 데이터 분석-지리 데이터 시각화"
tags: [data-analysis]
comments: true
---


![Image-1](../images/2019-11-20-Citibike-Data-Analysis-2-1.png){: .center-image}

```sql
SELECT
  left_side.*,
  middle_side.latitude as start_lat, 
  middle_side.longitude as start_lng,
  right_side.latitude as end_lat,
  right_side.longitude as end_lng
FROM `bigquery-public-data.austin_bikeshare.bikeshare_trips` AS left_side
LEFT JOIN `bigquery-public-data.austin_bikeshare.bikeshare_stations` AS middle_side
  ON left_side.start_station_id = middle_side.station_id
LEFT JOIN `bigquery-public-data.austin_bikeshare.bikeshare_stations` AS right_side
  ON left_side.end_station_id = right_side.station_id
```

