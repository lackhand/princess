---
layout: default
title: "Princess The RPG"
section: ""
---
# {{ page.title }} {#root}
{% assign sorted = site.pages | where_exp: 'item', 'item.section' | sort: 'section' %}

<details>
	<summary>Table of contents</summary>

	{% for page2 in sorted %}

	{% assign hLevel = page2.section | split: "." | size | minus: 1 | at_least: 1 %}
	{% assign hs = ""}
	{% for i in (2..hLevel) %}
		{% assign hs = hs | append: "  " %}
	{% endfor %}

	{{hs}}* {{page2.title}}](#{{ page2.url | slugify}})
	{% endfor %}
</details>

{% for page2 in sorted %}
{% if page2.url != page.url %}

{% assign hLevel = page2.section | split: "." | size | minus: 1 | at_least: 1 %}
{% assign hs = ""}
{% for i in (1..hLevel) %}
	{% assign hs = hs | append: "#" %}
{% endfor %}

{{hs}}# {{page2.title}} {#{{ page2.url | slugify }}}

{{page2.content}}

{% endif %}
{% endfor %}

<details>
	<summary>Raw documents & debug</summary>

	{% for page2 in sorted %}
	* [{{page2.section}}: {{page2.title}}]({{ page2.url }})
	{% endfor %}

</details>
