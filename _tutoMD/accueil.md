#### 1 index.md code image
```markdown
+++
date = '2025-03-13T18:27:35+01:00'
draft = false
title = ''
+++

<div class="hidden md:grid grid-cols-5 font-bold text-center justify-center items-center bg-mycolor-700">
    <div class="col-span-3">
        <h1 class="text-mywhite ">MA QUINCAILLERIE<br><br><span class="italic md:text-2xl lg:text-3xl xl:text-4xl 2xl:text-5xl">Au Vieux Caylus</span></h1>
    </div>
    <div class="col-span-2">
        <img  class="object-cover object-center " src="images/quincaillerieCarre.jpg" alt="La devanture de la Quincaillerie Au vieux Caylus" /> 
    </div>        
</div>

<div class="md:hidden bg-mycolor-700 font-bold text-white text-center ">
        <img  class="object-cover object-center" src="images/quincaillerieRectangle.jpg" alt="L'intérieur de la quincaillerie Au vieux Caylus" /> 
        <h1 class="py-4 text-xl text-mywhite" style="letter-spacing: .3rem;">Ma Quincaillerie<br><span class="text-base italic" style="letter-spacing: .15rem;">Au Vieux Caylus</span></h1>
</div>
```

#### 2 shortcodes/srcsetInAssets.html
```html
<!-- Traitement d'une image qui est dans assets/images  -->
<!-- voir https://mijndertstuij.nl/posts/hugo-responsive-images/ -->
<!-- Voir https://www.brycewray.com/posts/2022/06/responsive-optimized-images-hugo/ -->
<!-- Voir https://www.markusantonwolf.com/blog/guide-for-different-ways-to-access-your-image-resources/ -->
<!-- Attention : ici il faut dans $src metre print f"%s%s" et non pas "%s" -->

{{- $respSizes := slice "320" "640" "960" "1280" "1600" "1920" -}}
{{- $imgBase := "images/" -}}
{{- $src := resources.GetMatch (printf "%s%s" $imgBase (.Get "src")) -}}
{{- $alt := .Get "alt" -}}
{{- $divClass := "" -}}{{/* Init'g */}}
{{- $imgClass := "w-full h-auto animate-fade" -}}
{{- $dataSzes := "(min-width: 1024px) 100vw, 50vw" -}}
{{- $actualImg := $src.Resize "640x jpg" -}}
<picture>
  <source
    type="image/webp"
    srcset="
      {{- with $respSizes -}}
        {{- range $i, $e := . -}}
        {{- if ge $src.Width . -}}
          {{- if $i }}, {{ end -}}{{- ($src.Resize (printf "%sx%s" . " webp") ).RelPermalink }} {{ . }}w
        {{- end -}}
      {{- end -}}
    {{- end -}}"
    sizes="{{ $dataSzes }}"
  />
  <source
    type="image/jpeg"
    srcset="
      {{- with $respSizes -}}
        {{- range $i, $e := . -}}
          {{- if ge $src.Width . -}}
            {{- if $i }}, {{ end -}}{{- ($src.Resize (printf "%sx%s" . " jpg") ).RelPermalink }} {{ . }}w
          {{- end -}}
      {{- end -}}
    {{- end -}}"\
    sizes="{{ $dataSzes }}"
  />
  <img class="{{ $imgClass }}"
    src="{{ $actualImg.RelPermalink }}"
    width="{{ $src.Width }}"
    height="{{ $src.Height }}"
    alt="{{ $alt }}"
    loading="lazy"
  />
</picture>
```