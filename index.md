---
layout: home
title: Home
landing-title: Welcome to Stationary Action
description: 
image: 
author: 
nav-menu: 
---

<!-- Banner -->
<section id="banner" class="major">
	<div class="inner">
		<header class="major">
			<h1>{{ page.landing-title }}</h1>
		</header>
		<div class="content">
			<p style="text-transform: uppercase;">{{ site.description }}</p>
            <p></p>
			<ul class="actions">
				<li><a href="#one" class="button next scrolly">Get Started</a></li>
			</ul>
		</div>
	</div>
</section>

<!-- Main -->
<div id="main">

    <!-- One -->
    {% include tiles.html %}

    <!-- section id="two">
        <div class="inner">
            <header class="major">
                <h2>Blog</h2>
            </header>

            {% for post in site.posts limit:site.tiles-count %}
                <article>
                    <p><a href="{{ site.baseurl }}{{ post.url }}" class="link">{{ post.title }}</a></p>
                    <p>{{ post.description }}</p>
                < header class="major"></header>
                </article>
            {% endfor %}

            <ul class="actions">
                <li><a href="landing.html" class="button next">Go to Landing</a></li>
            </ul>
        </div>
    </section -->
     
</div>

