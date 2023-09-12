# Media Streaming (Implementation details)

## RTP
* RTP is one of the many ways to implement media stream. In RTP Header, there are some important fields: (i) Timestamp, (ii) Sequence Number, (iii) Syncronization source and (iv) Marker Flag.

* `Timestamp` is used to calculate the presentation clock on the destiny side. In fragmentation unit (A or B), it can also be used as an Identifier. A single video (H.264) stream packet will be split into multiples RTP packets. Each packet will have the same timestamp and thus it can be used as ID of the packet by the destiny to rebuild the packet.

* `Sequence Number` is a monotonic (incremental) number. Each packet sent increments the sequence number by 1. You can use Timestamp (as ID) and sequence number to rebuild the packet on arrival.

## H.264
* `NAL`or `NALU` could be interpreted as the "video frame" in packet format. A Video frame is initially encoded as a "String Of Data Bits" (SODB), which is not byte-aligned (it can be less than 8-bits/1-byte). When you fill the remaining missing bits (a trailing of zeros, and just to be more clear, at the end of the packet) to form a byte-aligned stream of bytes, you have a Raw Byte Sequence Payload (RBSP). However, inside the packet any sequence of bytes could appear. When you remove 0x000000, 0x000001 and 0x000003 from within the packet (by adding '0x000300' to any of the aforementioned byte sequence, e.g. 0x000001 => 0x000301, also known as the `emulation_preventio_three_byte`) then you have a NAL unit (packet).

* `Elementary Stream` (ES) is the most basic part of a stream (audio, video, etc). For instance, in H.264, an ES would be a stream of NALUs or using the RFC-3984 term: a "naked"
   H.264 NAL unit stream.

* `Annex B` is a bundle format of NALUs for network streaming. it is prefixed by 0x000001 (3-bytes) or 0x00000001 (4-bytes). More information can be found [here](https://stackoverflow.com/questions/24884827/possible-locations-for-sequence-picture-parameter-sets-for-h-264-stream/24890903#24890903) and [here](https://stackoverflow.com/questions/29525000/how-to-use-videotoolbox-to-decompress-h-264-video-stream/29525001#29525001). The prefix helps to parse the packet fast because you can use it to find where the packet ends.

* [`RFC-3984`](https://www.rfc-editor.org/rfc/rfc3984) When you combine H.264 and RTP, according to the this RFC, you must not use Annex B, only elementary stream of "naked"
   H.264 NAL unit stream. There are many ways of transmitting the video, but the most important one is probablt the fragmentation unit (FU) A. You basically take the frame and split into many RTP packets. Each packet will have the same Timestamp but different Sequence number and you can use both to rebuild the original packet. In FU-A, you add a FU indicator and a FU header in the begining of each packet. You must remove the original NALU header (1-byte). The content of the original NALU header is split between FU indicator and FU header plus some extra information related to FU itself.

* To rebuild the packet, you must pay attention to UDP quirks like: packet lost and reordering. You should also implement a jitter buffer, to reduce jitter (i.e. variation in latency).

## Media Foundation
* It does support to receive Annex B and Elementary Stream but it *cannot* generate Elementary Stream, only Annex B.

* From my experience not feasable to implement live streaming, it is too slow to produce (encode) packets. I do not recommend.

## Interesting sources

* [H.264 stream structure](https://wenchy.github.io/blogs/2015-12-11-H.264-stream-structure.html)
* [RTP Timestamp Calculation](https://lmtools.com/content/rtp-timestamp-calculation)
* [Multiple Packetization Times in the Session Description Protocol](https://www.ietf.org/archive/id/draft-garcia-mmusic-multiple-ptimes-problem-03.html)
* [H264 - what, why and how](https://membrane.stream/learn/h264/6)
* [Apple's video showcasing their library but it also has some interesting information](https://developer.apple.com/videos/play/wwdc2014/513/)
