---
title: "Live ship detection at Busan harbor"
date: "2019-06-01T23:27:18+09:00"
categories:
  - Posts
tags:
  - gotocloud
source: "https://gotocloud.co.kr/?p=1923"
---

> 📺 [YouTube](https://www.youtube.com/embed/H6h2szeba2Y?enablejsapi=1&autoplay=0&cc_load_policy=0&cc_lang_pref=&iv_load_policy=1&loop=0&rel=1&fs=1&playsinline=0&autohide=2&theme=dark&color=red&controls=1&disablekb=0&)

1280×720 30 fps live video from drone is streamed, and ships of Busan harbor are detected live in 10 FPS on GPU VM on AWS Oregon region using ImageAI python library

- Object Detection : ImageAI

- Compute Instance : AWS p3.2xlarge ( 1 V100 GPU / 4 physical CPU )

- Video transmitted by LTE network
