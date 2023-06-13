# Media Streaming (Implementation details)

## RTP
* Media streaming is usually implemented using RTP. In RTP Header there are some important fields to fill. (i) Timestamp, (ii) Sequence Number and (iii) Syncronization source and (iv) Marker Flag.

* `Timestamp` is used to calculate the presentation clock on the destiny side. It is also used as an Identifier. A single  video (H.264) stream can be split into multiples RTP packets. Each packet will have the same timestamp and thus it can be used as ID of the packet by the destiny to rebuild the packet.

* Sequence Number is a monotonic (incremental) number. Each packet sent increments the sequence number by 1. You can use Timestamp (as ID) and sequence number to rebuild the packet on arrival.


## Interesting sources

* [H.264 stream structure](https://wenchy.github.io/blogs/2015-12-11-H.264-stream-structure.html)
* [RTP Timestamp Calculation](https://lmtools.com/content/rtp-timestamp-calculation)
* [Multiple Packetization Times in the Session Description Protocol](https://www.ietf.org/archive/id/draft-garcia-mmusic-multiple-ptimes-problem-03.html)
