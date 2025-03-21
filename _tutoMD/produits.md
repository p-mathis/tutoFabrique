#### 1 list.html
```html
{{ define "main" }}
  <h1>{{ .Title }}</h1>
  {{ .Content }}
  {{ range .Pages }}
    <h2><a href="{{ .RelPermalink }}">{{ .Title }}</a></h2>
  {{ end }}
{{ end }}

```
#### 2 archetypes/produits.md
```markdown
+++
date = '{{ .Date }}'
draft = false
title = ''
photo = ''
alt = ''
rayon = ''
numero = ''
+++

## Description

## Commentaire

```