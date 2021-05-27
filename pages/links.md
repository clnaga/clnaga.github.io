---
layout: mypost
title: 友情链接
---


```
名称：{{ site.title }}
描述：{{ site.description }}
```

<ul>
  {%- for link in site.links %}
  <li>
    <p><a href="{{ link.url }}" title="{{ link.desc }}" target="_blank" >{{ link.title }}</a></p>
  </li>
  {%- endfor %}
</ul>
