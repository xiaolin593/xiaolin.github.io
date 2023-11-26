---
layout: default
---

<h1 class="post-title p-name" itemprop="name headline">Xiaolin Lin</h1>

## Distributed System and Data Analytics

<table style='table-layout:fixed; border:none; border-collapse:collapse; cellspacing:0; cellpadding:0'>
<tr>
<td width="20%" style='border:none; vertical-align: top;'> <img src="{{site.photo}}" alt="my photo" /> </td>
<td style="border:none">
Hi! I'm a software engineer on the fields of Distributed System and Data Analytics. I'm currently focusing on data analytic and processing with <a href="https://flink.apache.org/">Apache Flink</a> and Kafka. Prior to this, I worked at Cloud Storage team that builds in-house S3-like object storage backed by Ceph to support TBs data at Bloomberg LP. Before that, I was a software engineer at <a href="https://www.pandora.com/">Pandora Music</a> focused on music recommendation, discovery and machine learning.
</td>
</tr></table> 

<!-- CSS of table defined in _includes/head.html -->
<div class="Rtable Rtable--3cols Rtable--collapse">
  <!-- <div class="Rtable-cell"> <a href="{{site.resume}}"><i class="far fa-file">&nbsp;</i>resume</a> </div> -->
  <div class="Rtable-cell"> <a href="mailto:{{ site.author.email }}?subject=Hello"><i class="far fa-envelope" title="Email">&nbsp;</i>{{site.author.email}}</a> </div>
  <div class="Rtable-cell"> <a href="https://www.linkedin.com/in/{{ site.linkedin_username }}"> <i class="fab fa-linkedin" >&nbsp;</i>{{ site.linkedin_username }}</a> </div>
  <div class="Rtable-cell"> <a href="https://github.com/{{ site.github_username }}"><i class="fab fa-fw fa-github" >&nbsp;</i>{{ site.github_username}}</a> </div>
  <div class="Rtable-cell"> <a href="{{ site.url }}"><i class="fas fa-mouse-pointer">&nbsp;</i>{{site.url | replace:'http://','' | replace:'https://','' }}</a> </div>
</div>



<table style='border:none; border-collapse:collapse; cellspacing:0; cellpadding:0'>
{%- assign date_format = site.minima.date_format | default: "%Y" -%}
{% for post in site.posts %}
<tr>
<td class="align-top" style="border:none">
{{ post.date | date: date_format }}
</td>
<td class="align-top" style="border:none">
<a href="{{ post.url }}">{{ post.title }}</a>
</td>
</tr>
{% endfor %}
</table>
