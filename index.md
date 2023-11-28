---
layout: base
title: Home
hide: true
---

{% include nav_home.html %}

{% assign sprite_file = site.baseurl | append: page.image %}  <!--- Liquid concatentation --->
{% assign hash = site.data.mario_metadata %}  <!--- Liquid list variable created from file containing mario metatdata for sprite --->
{% assign pixels = 256 %} <!--- Liquid integer assignment --->

```
          _____                                                                _____ 
          ( ___ )                                                              ( ___ )
          |   |~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~|   | 
          |   |   ____   ____    ____    _____     _____          _     ____   |   | 
          |   |  / ___| / ___|  / ___|  | ____|   |_   _|  _ __  (_)   |___ \  |   | 
          |   | | |     \___ \  \___ \  |  _|       | |   | '__| | |     __) | |   | 
          |   | | |___   ___) |  ___) | | |___      | |   | |    | |    / __/  |   | 
          |   |  \____| |____/  |____/  |_____|     |_|   |_|    |_|   |_____| |   | 
          |___|~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~|___| 
          (_____)                                                              (_____)
```