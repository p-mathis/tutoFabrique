#### 0 tailwind.config.js
```js
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: ["./content/**/*.md", "./content/**/*.html", "./layouts/**/*.html"],  
  theme: {
    extend: {},
  },
  plugins: [],
}
```

#### 00 tailwind.css
```css
@tailwind base; 
@tailwind components; 
@tailwind utilities;
```

#### 000 commande npx
```bash
npx tailwindcss -i ./static/css/tailwind.css -o ./static/css/main.css –watch
```

#### 1 baseof.html
```html
<!DOCTYPE html >
<html lang="{{.Site.LanguageCode}}">
<head></head>
<body>
    {{ block "main" . }}
    {{ end }}
</body>
</html>
```

#### 2 _index.md 
```markdown
# Lorem Ipsum
## Paragraphe 1
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec vel velit eu mauris euismod maximus. Vestibulum sed erat lectus. Nam ex orci, imperdiet at felis eget, tempor iaculis nunc. Pellentesque a justo augue. In non tincidunt nisl. Etiam semper ante vel varius porta. In sit amet suscipit turpis. Interdum et malesuada fames ac ante ipsum primis in faucibus. Aliquam erat volutpat. Nunc tincidunt convallis aliquet.
## Paragraphe2
Cras condimentum ullamcorper nibh quis elementum. Etiam id lectus nisl. Praesent vitae dui elementum, dapibus ipsum in, pellentesque diam. Mauris quis ligula blandit, consectetur erat eu, finibus mi. Ut laoreet suscipit purus, nec euismod ante porttitor finibus. Nunc placerat purus sit amet aliquam bibendum. Mauris rutrum lobortis pharetra. Curabitur suscipit sapien vel blandit ullamcorper.
```

#### 3 index.html
```html
{{ define "main" }}
  <main aria-role="main">
      {{ .Content }}
  </main>
{{ end }}
```

#### 4 head.html
```html
<head>    
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
    <title>{{ if .Page.Title}}{{ .Page.Title }}{{else}}{{ .Site.Title}}{{end}}</title>

    <link rel="stylesheet" href="{{ .Site.BaseURL }}/css/main.css">    
  </head>
```

#### 5 baseof.html
```html
<!DOCTYPE html>
<html lang="{{.Site.LanguageCode}}">
  {{ block "head" .}} 
    {{ partial "head.html" .}}
  {{ end }}
  <body>
    {{ block "main" . }}
    {{ end }}
  </body>
</html>
```

#### 6 tailwind.config.js
```js
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: ["./content/**/*.md", "./content/**/*.html", "./layouts/**/*.html"],
  theme: {
    extend: {
      colors: {
        mycolor: {
          50: '#F9FAFB',
          100: '#F3F4F6',
          200: '#E5E7EB',
          300: '#D1D5DB',
          400: '#9CA3AF',
          500: '#6B7280',
          600: '#4B5563',
          700: '#374151',
          800: '#1F2937',
          900: '#111827',

        DEFAULT: '#1F2937',
        },
        myblack: '#111827',
        mywhite: '#ffffff',
        myred: '#ff2222',
      }, 
    },
  },
  plugins: [],
}
```
#### 7 tailwind.css
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
}
```

#### 8 hugo.toml
```toml
baseURL = 'https://example.org/'
languageCode = 'fr-fr'
title = 'Ma Fabrique'

[markup]
  [markup.goldmark]
    [markup.goldmark.renderer]
      unsafe = true
```
