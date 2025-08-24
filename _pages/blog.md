---
layout: page
title: Blog
description: Essays, tutorials, research notes, and playful science — neatly organised.
permalink: /blog/
nav: true
nav_order: 4
toc: false

# Define your blog "sections" (these will become subpages at /blog/<slug>/)
sections:
  - name: General
    slug: quantum
    icon: fas fa-atom
    blurb: Blogs that don't quite fit any other category.
    color: primary
  - name: Quantum and Machine Learning
    slug: tutorials
    icon: fas fa-chalkboard-teacher
    blurb: Research explainers, code walk-throughs, and practical examples.
    color: info
  - name: A Miss You May Have Missed
    slug: lab-notes
    icon: fas fa-flask
    blurb: Day-to-day discoveries, debugging tales, and methods I wish I’d known sooner.
    color: success
  - name: Outreach & Teaching
    slug: outreach
    icon: fas fa-people-group
    blurb: Talks, course materials, and ideas for making science more accessible.
    color: warning
  - name: VR & Tools
    slug: vr-tools
    icon: fas fa-vr-cardboard
    blurb: VR experiments, interactive demos, and software I’m building.
    color: danger
  - name: Qubit the Cat
    slug: qubit-the-cat
    icon: fas fa-cat
    blurb: Updates and extras from my quantum colouring book project.
    color: secondary
---

<!-- Quick category buttons -->
<div class="d-flex flex-wrap gap-2 mb-4">
  {% for s in page.sections %}
    <a class="btn btn-{{ s.color }} btn-sm" href="{{ '/blog/' | append: s.slug | relative_url }}">
      <i class="{{ s.icon }}"></i> {{ s.name }}
    </a>
  {% endfor %}
  <a class="btn btn-outline-secondary btn-sm" href="#all-posts"><i class="fas fa-list-ul"></i> All posts</a>
</div>

<!-- Featured posts -->
{% assign featured = site.posts | where_exp: "p", "p.featured == true" | slice: 0, 3 %}
{% if featured and featured.size > 0 %}
  <h2 class="h4 mt-4 mb-3"><i class="fas fa-star me-2 text-warning"></i>Featured</h2>
  <div class="row">
    {% for post in featured %}
      <div class="col-md-4 mb-3">
        <div class="card h-100 shadow-sm">
          {% if post.thumbnail %}
            <img class="card-img-top" src="{{ post.thumbnail | relative_url }}" alt="{{ post.title }}">
          {% endif %}
          <div class="card-body">
            <h3 class="h5 card-title"><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h3>
            <p class="card-text text-muted small mb-2">{{ post.date | date_to_long_string }}</p>
            <p class="card-text">{{ post.excerpt | strip_html | truncate: 150 }}</p>
            {% if post.categories %}
              <div class="mt-2">
                {% for c in post.categories %}
                  <span class="badge rounded-pill text-bg-light me-1">{{ c }}</span>
                {% endfor %}
              </div>
            {% endif %}
          </div>
        </div>
      </div>
    {% endfor %}
  </div>
{% endif %}

<!-- Sections grid -->
<h2 class="h4 mt-4 mb-3"><i class="fas fa-folder-tree me-2"></i>Browse by section</h2>
<div class="row">
  {% for s in page.sections %}
    <div class="col-md-6 col-lg-4 mb-3">
      <a class="text-decoration-none" href="{{ '/blog/' | append: s.slug | relative_url }}">
        <div class="card h-100 border-0 shadow-sm">
          <div class="card-body">
            <span class="badge bg-{{ s.color }} mb-2"><i class="{{ s.icon }}"></i> {{ s.name }}</span>
            <p class="mb-0 text-body">{{ s.blurb }}</p>
          </div>
        </div>
      </a>
    </div>
  {% endfor %}
</div>

<!-- Latest posts -->
<h2 id="all-posts" class="h4 mt-4 mb-3"><i class="fas fa-clock me-2"></i>Latest</h2>
<div class="row">
  {% assign recent = site.posts | slice: 0, 12 %}
  {% for post in recent %}
    <div class="col-md-6 col-lg-4 mb-3">
      <div class="card h-100 shadow-sm">
        <div class="card-body">
          <h3 class="h5 card-title"><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h3>
          <p class="card-text text-muted small mb-2">{{ post.date | date_to_long_string }}</p>
          <p class="card-text">{{ post.excerpt | strip_html | truncate: 140 }}</p>
          {% if post.categories %}
            <div class="mt-2">
              {% for c in post.categories %}
                <span class="badge rounded-pill text-bg-light me-1">{{ c }}</span>
              {% endfor %}
            </div>
          {% endif %}
        </div>
      </div>
    </div>
  {% endfor %}
</div>

<!-- Tag cloud -->
{% if site.tags %}
  <h2 class="h4 mt-4 mb-3"><i class="fas fa-tags me-2"></i>Tags</h2>
  <div class="d-flex flex-wrap gap-2">
    {% assign tags = site.tags | sort %}
    {% for tag in tags %}
      {% assign name = tag[0] %}
      {% assign posts = tag[1] %}
      <a class="badge rounded-pill text-bg-secondary text-decoration-none" href="{{ '/tags/#' | append: name | relative_url }}">
        #{{ name }} <span class="small">({{ posts | size }})</span>
      </a>
    {% endfor %}
  </div>
{% endif %}
