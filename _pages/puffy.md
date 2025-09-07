---
layout: page
title: "Puffy"
permalink: /puffy/
author_profile: true
---

![Puffy1](/assets/images/puffy/puffy1.jpg)

Puffy 是我家的猫，18 斤，橘色，爱吃罐头……（在这里写一段故事/介绍）

更多照片：
{% for img in ["/assets/images/puffy/puffy1.jpg","/assets/images/puffy/puffy2.jpg","/assets/images/puffy/puffy3.jpg"] %}
  <img src="{{ img | relative_url }}" style="max-width:200px; margin-right:0.5rem;" />
{% endfor %}
