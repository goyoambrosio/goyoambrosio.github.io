---
layout: splash
permalink: /
header:
  overlay_color: "#5e616c"
  overlay_image: /assets/images/home1_1600x586.jpg
  # cta_label: "<i class='fa fa-download'></i> Install Now"
  # cta_url: "/docs/quick-start-guide/"
  caption:
excerpt: 'by Goyo Ambrosio'
feature_row:
  - image_path: /assets/images/mm-customizable-feature.png
    alt: "customizable"
    title: "Super Customizable"
    excerpt: "Everything from the menus, sidebars, comments, and more can be configured or set with YAML Front Matter."
    url: "/docs/configuration/"
    btn_label: "Learn More"
  - image_path: /assets/images/mm-responsive-feature.png
    alt: "fully responsive"
    title: "Responsive Layouts"
    excerpt: "Built on HTML5 + CSS3. All layouts are fully responsive with helpers to augment your content."
    url: "/docs/layouts/"
    btn_label: "Learn More"
  - image_path: /assets/images/mm-free-feature.png
    alt: "100% free"
    title: "100% Free"
    excerpt: "Free to use however you want under the MIT License. Clone it, fork it, customize it, whatever!"
    url: "/docs/license/"
    btn_label: "Learn More"
intro:
  - excerpt: 'Follow me &nbsp; [<i class="fa fa-twitter"></i> @gambrosio](https://twitter.com/gambrosio){: .btn .btn--twitter}'
---

{% include feature_row id="intro" type="center" %}

{% include sidebar.html %}

<h3 class="archive__subtitle">{{ site.data.ui-text[site.locale].recent_posts | default: "Recent Posts" }}</h3>

{% for post in paginator.posts %}
{% if post.header.teaser %}
  {% capture teaser %}{{ post.header.teaser }}{% endcapture %}
{% else %}
  {% assign teaser = site.teaser %}
{% endif %}

{% if post.id %}
  {% assign title = post.title | markdownify | remove: "<p>" | remove: "</p>" %}
{% else %}
  {% assign title = post.title %}
{% endif %}

<div class="{{ include.type | default: "list" }}__item">
  <article class="archive__item" itemscope itemtype="http://schema.org/CreativeWork">
    {% if include.type == "grid" and teaser %}
      <div class="archive__item-teaser">
        <img src=
          {% if teaser contains "://" %}
            "{{ teaser }}"
          {% else %}
            "{{ teaser | absolute_url }}"
          {% endif %}
          alt="">
      </div>
    {% endif %}
    <h2 class="archive__item-title" itemprop="headline">
      {% if post.link %}
        <a href="{{ post.link }}">{{ title }}</a> <a href="{{ post.url | absolute_url }}" rel="permalink"><i class="fa fa-link" aria-hidden="true" title="permalink"></i><span class="sr-only">Permalink</span></a>
      {% else %}
        <a href="{{ post.url | absolute_url }}" rel="permalink">{{ title }}</a>
      {% endif %}
    </h2>
    {% if post.read_time %}
      <p class="page__meta"><i class="fa fa-clock-o" aria-hidden="true"></i> {% include read-time.html %}</p>
    {% endif %}
    {% if post.excerpt %}<p class="archive__item-excerpt" itemprop="description">{{ post.excerpt | markdownify | strip_html | truncate: 160 }}</p>{% endif %}
  </article>
</div>



{% endfor %}

{% include paginator.html %}
