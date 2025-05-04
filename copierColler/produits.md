#### 1 archetypes/produits.md
```markdown
+++
date = '{{ .Date }}'
draft = false
title = ''
photo = '_default_image.jpg'
alt = ''
photoTitle = ''
photoComment = ''
numero = ''
description = ''
keywords = []
+++

## Notre Produit

## Nos Commentaires

```

#### 2 produits/list.html
```html
{{ define "main" }}

  {{ $image_title := .Page.Params.photoTitle }}
  {{ $image_comment := .Page.Params.photoComment }}
  
  <!-- titre et photo écran md et plus -->
  <div class="hidden md:grid grid-cols-5 font-bold text-center justify-center items-center bg-mycolor-700">
    
    <div class="col-span-3">
      <h1 class="text-mywhite uppercase">{{ $image_title }}<br><br><span class="italic md:text-2xl lg:text-3xl xl:text-4xl 2xl:text-5xl">{{ $image_comment }}</span></h1>
    </div>
    <div class="col-span-2">
      {{ partial "srcsetInAssets.html" . }}
    </div>        
  </div>
  <!-- titre et photo écran sm -->
  <div class="md:hidden bg-mycolor-700 font-bold text-white text-center ">
    {{ partial "srcsetInAssets.html" . }}
    <h1 class="py-4 text-xl text-mywhite uppercase" style="letter-spacing: .3rem;">{{ $image_title }}<br><span class="text-base italic" style="letter-spacing: .15rem;">{{ $image_comment }}</span></h1>
  </div>

  <!-- Content inutile si on n'écrit rien dans les _index.md 
   Décommenter si on veut voir le Content -->
  <!-- {{ .Content }} -->

  {{ range .Pages.ByTitle }}
    {{ $description := .Page.Params.description }}
    <!-- Pour portables -->
    <div class="grid md:hidden grid-cols-5  font-bold text-center justify-center items-center bg-mycolor-400 py-2 text-mycolor-700 ">
      <div class="col-span-1">
        <a href="{{ .RelPermalink }}">
          {{ partial "srcsetInAssets.html" . }}
        </a>
      </div>
      <div class="col-span-2 pl-4">
        <a href="{{ .RelPermalink }}">
          <h2 class="uppercase text-left ">{{ .Title }}</h2>
        </a>
      </div>
    </div>
    <!-- Pour md et plus -->
    <div class="hidden md:grid grid-cols-6 gap-x-2 font-bold text-center justify-center items-center bg-mycolor-400 py-2 text-mycolor-700 ">
      <div class="col-span-1">
        <a href="{{ .RelPermalink }}">
          {{ partial "srcsetInAssets.html" . }}
        </a>
      </div>
      <div class="col-span-2">
        <a href="{{ .RelPermalink }}">
          <h2 class="uppercase text-left ">{{ .Title }}</h2>
        </a>
      </div>
      <div class="col-span-3">
        <p class="text-left">{{ $description | markdownify }}</p>
      </div>
    </div>
  {{ end }}
{{ end }}
```

#### 3 produits/single.html SANS encart
```html
{{ define "main" }}
  <main aria-role="main">
    
    {{ $photo_title := .Page.Params.photoTitle }}
    {{ $photo_comment := .Page.Params.photoComment }}

    <!-- titre et photo écran md et plus -->
    <div class="hidden md:grid grid-cols-5 font-bold text-center justify-center items-center bg-mycolor-700">   
      <div class="col-span-3">
        <h1 class="text-mywhite uppercase">{{ .Title }}<br><br><span class="italic md:text-2xl lg:text-3xl xl:text-4xl 2xl:text-5xl">{{ $photo_comment }}</span></h1>
      </div>
      <div class="col-span-2">
        {{ partial "srcsetInAssets.html" . }}
      </div>        
    </div>
    <!-- titre et photo écran sm -->
    <div class="md:hidden bg-mycolor-700 font-bold text-white text-center ">
      {{ partial "srcsetInAssets.html" . }}
      <h1 class="py-4 text-xl text-mywhite uppercase" style="letter-spacing: .3rem;">{{ .Title }}<br><span class="text-base italic" style="letter-spacing: .15rem;">{{ $photo_comment }}</span></h1>
    </div>
    
    <!-- div pour le Content -->
    <div class="md:mt-2 md:pt-2 md:border-t-2 md:border-myred">
      {{ .Content }}
    </div>
    
  </main>
{{ end }}
```



#### 4 produits/single.html AVEC encart

```html
{{ define "main" }}
  <main aria-role="main">
    {{ $photo_title := .Page.Params.photoTitle }}
    {{ $photo_comment := .Page.Params.photoComment }}

    {{ $currentSection := .CurrentSection }}
    {{ $slice := split $currentSection "/" }}
    {{ $len := $slice | len }}
    {{ $index := math.Sub $len 2 }}
    {{ $rayon := index $slice $index }}

    <!-- titre et photo écran md et plus -->
    <div class="hidden md:grid grid-cols-5 font-bold text-center justify-center items-center bg-mycolor-700">
      
      <div class="col-span-3">
        <h1 class="text-mywhite uppercase">{{ .Title }}<br><br><span class="italic md:text-2xl lg:text-3xl xl:text-4xl 2xl:text-5xl">{{ $photo_comment }}</span></h1>
      </div>
      <div class="col-span-2">
        {{ partial "srcsetInAssets.html" . }}
      </div>        
    </div>
    <!-- titre et photo écran sm -->
    <div class="md:hidden bg-mycolor-700 font-bold text-white text-center ">
      {{ partial "srcsetInAssets.html" . }}
      <h1 class="py-4 text-xl text-mywhite uppercase" style="letter-spacing: .3rem;">{{ .Title }}<br><span class="text-base italic" style="letter-spacing: .15rem;">{{ $photo_comment }}</span></h1>
    </div>

    <!-- Encart pour décrire l'article -->
    <div class="pt-2 md:py-4">
      <div class="m-auto md:w-3/4  border-2 md:border-4 border-myred rounded-xl p-2 md:px-12 bg-gradient-to-r from-mycolor-400 via-mycolor-100 to-mycolor-600 text-left text-mycolor-900 font-bold">
        <span class="capitalize">{{ $photo_title }}</span><br>
        {{ $photo_comment }} <br>
        Rayon : <span class="capitalize">{{ $rayon }}</span> - Réf #{{ .Params.numero}}
      </div>
    </div>

    <!-- div pour le Content -->
    <div class="md:mt-2 md:pt-2 md:border-t-2 md:border-myred">
      {{ .Content }}
    </div>
    
  </main>
{{ end }}
```

