# gstreamer-1.0-to-html
webm

gst-launch-1.0 v4l2src device=/dev/video0 ! videoconvert ! videoscale ! video/x-raw,width=320,height=240 ! clockoverlay shaded-background=true font-desc="Sans 38" ! theoraenc ! oggmux ! tcpserversink host=127.0.0.1 port=8080
 

gst-launch-1.0 videotestsrc is-live=true ! clockoverlay shaded-background=true font-desc="Sans 38" ! x264enc ! mpegtsmux ! queue ! tcpserversink host=127.0.0.1 port=8080

reference to:

https://gist.github.com/azotlikid/edf05381740ff7213ac95f0cbbcd9ee6#file-streaming-linux-sh-L4

gst-launch-1.0 v4l2src device=/dev/video0 ! videoconvert ! videoscale ! video/x-raw,width=320,height=240 ! clockoverlay shaded-background=true font-desc="Sans 38" ! theoraenc ! oggmux ! tcpserversink host=127.0.0.1 port=8080 


gst-launch-1.0 v4l2src device=/dev/video0 ! vp8enc ! webmmux streamable=true name=stream ! tcpserversink host=localhost port=8080

gst-launch-1.0 autovideosrc horizontal-speed=1 is-live=true ! videoconvert ! vp8enc cpu-used=5 deadline=1 keyframe-max-dist=10 ! queue leaky=1 ! m. autoaudiosrc ! audioconvert ! vorbisenc ! queue leaky=1 ! m. webmmux name=m streamable=true ! queue leaky=1 ! tcpserversink host=127.0.0.1 port=9001 sync-method=2

