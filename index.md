---
layout: default
title: "Princess The RPG"
section: ""
---

# {{ page.title }} {#root}
{% assign sorted = site.pages | where_exp: 'item', 'item.section' | sort: 'section' %}
{%- comment -%}
Think VERY hard before editing this file.
The whitespace below, particularly around list elements, is INCREDIBLY significant.
(this is flagged with the missing `{ % -` sequence on the `endfor`).
ditto the two level print-then-execute, to ensure each line of <li> is captured in the same <ul>.
{%- endcomment -%}

<details open>
	<summary>Table of contents</summary>

{% capture toc -%}
	{%- for page2 in sorted -%}
	{%- assign hLevel = page2.section | split: "." | size | minus: 1 | at_least: 1 -%}
	{%- assign hs = "" -%}
	{%- for i in (2..hLevel) -%}
		{%- capture hs %}  {{hs}}{% endcapture -%}
	{%- endfor -%}
{{ hs }}* [{{ page2.title }}](#{{ page2.url | slugify}})
{% endfor -%}
{%- endcapture -%}

{{ toc | liquify | markdownify }}

</details>

{% for page2 in sorted -%}
{%- if page2.url != page.url -%}
{%- assign hLevel = page2.section | split: "." | size | minus: 1 | at_least: 1 -%}
{%- assign hs = "" -%}
{%- for i in (2..hLevel) -%}
	{%- capture hs %}#{{hs}}{% endcapture -%}
{%- endfor -%}

{{ hs }}# [{{ page2.title }}](#{{ page2.url | slugify }}) {#{{ page2.url | slugify }}}

{{ page2.content }}

{%- endif -%}
{%- endfor %}

<details>
	<summary>Raw documents & debug</summary>

{% capture toc -%}
	{%- for page2 in sorted -%}
* [{{page2.section}}: {{page2.title}}]({{ page2.url | absolute_url }})
{% endfor -%}
{%- endcapture -%}

{{ toc | liquify | markdownify }}

</details>
