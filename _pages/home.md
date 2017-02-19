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

<div id="main" role="main">
  <div class="article-author-side">
    {% include _author-bio.html %}
  </div>
  <div id="index">
    <h3><a href="{{ site.url}}/posts/">Recent Posts</a></h3>
    {% for post in site.posts limit:5 %}
    <article>
      {% if post.link %}
        <h2 class="link-post"><a href="{{ site.url }}{{ post.url }}" title="{{ post.title }}">{{ post.title }}</a> <a href="{{ post.link }}" target="_blank" title="{{ post.title }}"><i class="fa fa-link"></i></a></h2>
      {% else %}
        <h2><a href="{{ site.url }}{{ post.url }}" title="{{ post.title }}">{{ post.title }}</a></h2>
        <p>{{ post.excerpt | strip_html | truncate: 160 }}</p>
      {% endif %}
    </article>
    {% endfor %}
  </div><!-- /#index -->
</div><!-- /#main -->
