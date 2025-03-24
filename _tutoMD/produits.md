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
keywords = []
+++

## Description

## Commentaire

```
#### 3 produits/single.html
```html
{{ define "main" }}
  <main aria-role="main">

    {{ if .Page.Title }}<h1 class="uppercase text-center pt-8 pb-10 lg:pt-20 lg:pb-24 bg-mycolor-900 text-myred">{{ .Page.Title }}</h1>
    {{ end }}

    <div class="bg-mycolor-500 pt-8">
      <div class="text-center  py-8">
        <h2 class="text-mywhite uppercase">{{ .Page.Params.Rayon}}</h2>  
        </div>
    </div>
    <div class="bg-myred pt-8">
      <div class="text-left  py-4">
        <h3 class="text-myblack uppercase pl-8">Référence : {{ .Page.Params.Numero}}</h2>  
        </div>
    </div>
    {{ .Content }}

  </main>
{{ end }}
```
#### 4 produits/single.html (Version complète)
```html
{{ define "main" }}
  <main aria-role="main">
    {{ if .Page.Title }}<h1 class="uppercase text-center pt-8 pb-10 lg:pt-20 lg:pb-24 bg-mycolor-900 text-myred">{{ .Page.Title }}</h1>
    {{ end }}

    {{$src := resources.Get (print "images/" .Params.Photo)}}
    {{$alt :=  .Params.Alt }}

    {{ .Scratch.Set "src" $src}}
    {{ .Scratch.Set "alt" $alt}}

    <div class="bg-mycolor-500 pt-8">
      <div class="mx-auto w-5/12 md:w-4/12 lg:w-3/12">

      {{ partial "srcsetInAssets.html" . }}

      </div>
      <div class="text-center  py-8">

        <h2 class="text-mywhite uppercase">{{ .Page.Params.Rayon}}</h2>
  
        </div>
    </div>
    
    <div class="bg-myred pt-8">
      <div class="text-left  py-4">
        <h3 class="text-myblack uppercase pl-8">Référence : {{ .Page.Params.Numero}}</h2>  
        </div>
    </div>  
    {{ .Content }}
  </main>
{{ end }}
```