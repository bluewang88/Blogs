```sequence
UAC->UAS:sip:invite(SDP Offer)
UAS->UAC:100Trying
UAS->UAC:180Ring
UAS->UAC:200 OK(SDP Answer)
UAC->UAS:ACK
UAC->UAS:RTP
UAS->UAC:RTP
```