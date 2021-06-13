---
title: "{{ replace .Name "-" " " | title }}"
date: {{ .Date }}
categories: {{ range $name, $taxonomy := .Site.Taxonomies }}{{ if eq $name "categories" }}[{{ range $key, $value := $taxonomy }}
	{{ $key }},{{ end }}
]{{ end }}{{ end }}
tags: {{ range $name, $taxonomy := .Site.Taxonomies }}{{ if eq $name "tags" }}[{{ range $key, $value := $taxonomy }}
	{{ $key }},{{ end }}
]{{ end }}{{ end }}
summary: ""
author: {{ .Site.Params.author }}
img: 
draft: true
---

content
