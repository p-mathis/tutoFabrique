#### 1 nav.html Menu simple
```html
<nav class="bg-mycolor-500 text-white font-bold text-center">
    <ul class="list-none">
        <li class="hover:text-myred hover:scale-125"><a class="no-underline" href="/">Accueil</a></li>
        <li class="hover:text-myred hover:scale-125"><a class="no-underline " href="/histoire">Histoire</a></li>
    </ul>
</nav>
```

#### 2 layouts/_default/baseof.html
```html
<!DOCTYPE html>
<html lang="{{.Site.LanguageCode}}">
  {{ block "head" .}} 
    {{ partial "head.html" .}}
  {{ end }}
  <body>
    {{ block "nav" .}}
      {{ partial "nav.html" .}}
    {{ end }}
    
    {{ block "main" . }}
    {{ end }}
  </body>
</html>
```
