# Exporter User Guide

## Environment Variables
* API_SECRET - BigBlueButton API Secret
    * **Required: true**
    * Use `$ bbb-conf --secret` on BigBlueButton server to get secret and Base API url
* API_BASE_URL - BigBlueButton API base URL
    * **Required: true**
    * Example: "https://example.com/bigbluebutton/api/"
    * Trailing slash is required!
    * Make sure you supply the base url **of the API**, often this URL ends in `/api/`
* DEBUG - Enable debug logging
    * Required: false
    * Default: false
    * Values: &lt;true | false&gt;
* RECORDINGS_METRICS - Enable collection of recordings metrics 
    * Required: false
    * Default: true
    * Values: &lt;true | false&gt;
* BIND_IP - Which network address to bind the HTTP server of the exporter
    * Required: false
    * Default: 0.0.0.0
* PORT - HTTP port to serve the exporter metrics
    * Required: false
    * Default: 9688
    * Values: &lt;1 - 65535&gt;
    
### Metric Histogram Custom Buckets
* ROOM_PARTICIPANTS_CUSTOM_BUCKETS - Custom bucket sizes for the `bbb_room_participants_bucket` histogram metric
    * Required: false
    * Default: `0,1,5,15,30,60,90,120,150,200,250,300,400,500`
    * `INF` will be added automatically as the final bucket size
    * Values: list of integers separated using comma (`,`)
    
* ROOM_LISTENERS_CUSTOM_BUCKETS - Custom bucket sizes for the `bbb_room_listeners_bucket` histogram metric
    * Required: false
    * Default: `0,1,5,15,30,60,90,120,150,200,250,300,400,500`
    * `INF` will be added automatically as the final bucket size
    * Values: list of integers separated using comma (`,`)
* ROOM_VOICE_PARTICIPANTS_CUSTOM_BUCKETS - Custom bucket sizes for the `bbb_room_voice_participants_bucket` histogram 
metric
    * Required: false
    * Default: `0,1,5,15,30,60,90,120`
    * `INF` will be added automatically as the final bucket size
    * Values: list of integers separated using comma (`,`)
* ROOM_VIDEO_PARTICIPANTS_CUSTOM_BUCKETS - Custom bucket sizes for the `bbb_room_video_participants_bucket` histogram 
metric
    * Required: false
    * Default: `0,1,5,15,30,60,90,120`
    * `INF` will be added automatically as the final bucket size
    * Values: list of integers separated using comma (`,`)
    
## Metrics
### Gauges
* bbb_meetings_participants - Total number of participants in all BigBlueButton meetings
* bbb_meetings_listeners - Total number of listeners in all BigBlueButton meetings
* bbb_meetings_voice_participants - Total number of voice participants in all BigBlueButton meetings
* bbb_meetings_video_participants - Total number of video participants in all BigBlueButton meetings
* bbb_meetings_participant_clients(type=<client\>) - Total number of participants in all BigBlueButton meetings by client (html5|dial-in|flash)
* bbb_recordings_processing - Total number of BigBlueButton recordings processing
* bbb_recordings_processed - Total number of BigBlueButton recordings processed
* bbb_recordings_published - Total number of BigBlueButton recordings published
* bbb_recordings_unpublished - Total number of BigBlueButton recordings unpublished
* bbb_recordings_deleted - Total number of BigBlueButton recordings deleted
* bbb_api_up - 1 if BigBlueButton API is responding 0 otherwise
* bbb_exporter(labels: version) - Information about the exporter (i.e. version)

### Histograms
* bbb_api_latency(labels: endpoint, parameters) - BigBlueButton API call latency
    * buckets: .01, .025, .05, .075, .1, .25, .5, .75, 1.0, 1.25, 1.5, 1.75, 2.0, 2.5, 5.0, 7.5, 10.0, INF
* bbb_room_participants_bucket - Number of rooms with participants less than or equal to the bucket size
    * buckets: 0, 1, 5, 15, 30, 60, 90, 120, 150, 200, 250, 300, 400, 500, INF
    * bucket sizes can be overridden using `ROOM_PARTICIPANTS_CUSTOM_BUCKETS`, see 
    [environment variables - metric-histogram-custom-buckets](#metric-histogram-custom-buckets) for details
* bbb_room_listeners_bucket - Number of rooms with listeners less than or equal to the bucket size
    * buckets: 0, 1, 5, 15, 30, 60, 90, 120, 150, 200, 250, 300, 400, 500, INF
    * bucket sizes can be overridden using `ROOM_LISTENERS_CUSTOM_BUCKETS`, see 
    [environment variables - metric-histogram-custom-buckets](#metric-histogram-custom-buckets) for details
* bbb_room_voice_participants_bucket - Number of rooms with voice participants less than or equal to the bucket size
    * buckets: 0, 1, 5, 15, 30, 60, 90, 120, INF
    * bucket sizes can be overridden using `ROOM_VOICE_PARTICIPANTS_CUSTOM_BUCKETS`, see 
    [environment variables - metric-histogram-custom-buckets](#metric-histogram-custom-buckets) for details
* bbb_room_video_participants_bucket - Number of rooms with video participants less than or equal to the bucket size
    * buckets: 0, 1, 5, 15, 30, 60, 90, 120, INF
    * bucket sizes can be overridden using `ROOM_VIDEO_PARTICIPANTS_CUSTOM_BUCKETS`, see 
    [environment variables - metric-histogram-custom-buckets](#metric-histogram-custom-buckets) for details
