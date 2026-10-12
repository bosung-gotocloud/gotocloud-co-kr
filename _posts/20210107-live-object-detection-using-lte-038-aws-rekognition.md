---
title: "Live object detection using LTE &#038; AWS rekognition"
date: "2021-01-07T00:28:14+09:00"
categories:
  - Posts
tags:
  - gotocloud
source: "https://gotocloud.co.kr/?p=1937"
---

> 📺 [YouTube](https://www.youtube.com/embed/vQR5pfjai3Y?enablejsapi=1&autoplay=0&cc_load_policy=0&cc_lang_pref=&iv_load_policy=1&loop=0&rel=1&fs=1&playsinline=0&autohide=2&theme=dark&color=red&controls=1&disablekb=0&)

Live object detection prototype is built on AWS cloud using Rekognition service with LTE network. A Video is sent to AWS cloud and objects in the video are detected. Result video is streamed by RTMP.

Time delay between the original video and the detected video occurs  by the various reasons.

- LTE transmission time

- Time for conversion from video to image

- Time delay due to the video streaming
