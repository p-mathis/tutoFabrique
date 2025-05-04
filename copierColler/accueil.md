#### 1 _index.md code image
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

#### 3 _index.md shortcode image
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
        {{< images/srcsetInAssets src="quincaillerieCarre.jpg" alt="la devanture de la quincaillerie au vieux caylus" >}}
    </div>        
</div>

<div class="md:hidden bg-mycolor-700 font-bold text-white text-center ">
    {{< images/srcsetInAssets src="quincaillerieRectangle.jpg" alt="L'intérieur de la quincaillerie au vieux caylus" >}}
    <h1 class="py-4 text-xl text-mywhite" style="letter-spacing: .3rem;">Ma Quincaillerie<br><span class="text-base italic" style="letter-spacing: .15rem;">Au Vieux Caylus</span></h1>
</div>
```
#### 4 _index.md shortcode texte
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
        {{< images/srcsetInAssets src="quincaillerieCarre.jpg" alt="la devanture de la quincaillerie au vieux caylus" >}}
    </div>        
</div>

<div class="md:hidden bg-mycolor-700 font-bold text-white text-center ">
    {{< images/srcsetInAssets src="quincaillerieRectangle.jpg" alt="L'intérieur de la quincaillerie au vieux caylus" >}}
    <h1 class="py-4 text-xl text-mywhite" style="letter-spacing: .3rem;">Ma Quincaillerie<br><span class="text-base italic" style="letter-spacing: .15rem;">Au Vieux Caylus</span></h1>
</div>

{{< text/lightViaDark >}}
## Lorem Ipsum
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Fusce nec velit a ante lacinia interdum. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Mauris ac justo diam. Sed lorem enim, elementum at sodales ut, vulputate non nibh. In id magna non lacus cursus ornare in vestibulum neque. Curabitur congue viverra posuere. Mauris vitae dolor at ipsum dictum consectetur feugiat in turpis. Cras quis lacus pretium, rhoncus sem elementum, aliquam augue. Quisque suscipit congue nulla a commodo. In hac habitasse platea dictumst. Curabitur ullamcorper, est at bibendum facilisis, ligula ante aliquam tortor, quis aliquam nisl lacus eu sapien.
{{< /text/lightViaDark >}}
{{< text/darkViaLight >}}
## Ut a lacinia diam
Ut a lacinia diam, pellentesque dictum lorem. Nam tristique sit amet nunc nec ornare. Nulla tellus lacus, varius in massa eu, vestibulum ultricies est. Nulla sit amet leo odio. Pellentesque vestibulum libero sit amet fermentum condimentum. Nulla maximus dui ut mauris viverra, sit amet imperdiet arcu sagittis. Ut nec orci eros. Ut auctor dapibus ex in hendrerit.
{{< /text/darkViaLight >}}
```
#### 5 single.html
```html
{{ define "main" }}
  <main aria-role="main">
    {{ if .Page.Title }}<h1 class="uppercase text-center pt-8 pb-10 lg:pt-20 lg:pb-24 bg-mycolor-600 text-mywhite">{{ .Page.Title }}</h1>
    {{ end }}
    {{ .Content }}
  </main>
{{ end }}
```

#### 6 histoire/index.md

```markdown
+++
date = '2025-03-18T23:26:01+01:00'
draft = false
title = 'Notre Histoire !'
+++

{{< typo/spaceLine >}}
{{< text/lightViaDark >}}
## Une belle histoire !
Une quincaillerie au long passé, qui vous propose :
- des clous
- des vis
- de la peinture
{{< /text/lightViaDark >}}
{{< typo/spaceLine >}}

{{< images/srcsetInPage src="histoire-quincaillerie.jpg" alt="l'intérieur d'une quincaillerie" >}}
```

#### 7 tailwind.css liste et ancre
```css
@tailwind base;
@tailwind components;
@tailwind utilities;

@layer base {

  /* le body */
  body {
    @apply bg-mycolor-200 text-mycolor-700 px-1 md:px-2;
  }

  /* les titres */
  h1 {
    @apply text-2xl  font-semibold py-2 ;  
    @apply md:text-3xl md:py-6;    
    @apply lg:text-4xl lg:py-12;   
    @apply xl:text-5xl xl:py-20;   
    @apply 2xl:text-6xl 2xl:py-24;  
  }
  
  h2 {
    @apply text-2xl font-medium pt-3 pb-1.5;
  }
  h3 {
    @apply text-xl font-medium py-1.5;
  }
  h4 {
    @apply text-base font-medium italic py-1.5;
  }
  /* les puces */
  ul {
    @apply list-inside list-disc;
  }
  
  /* les ancres souligner */
  a {
    @apply underline;
    }
    
}
```