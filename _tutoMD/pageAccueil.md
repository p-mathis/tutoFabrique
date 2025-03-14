#### 1 baseof.html
```html
<!DOCTYPE html >
<html>
<head></head>
<body>
    {{ block "main" . }}
    {{ end }}
</body>
</html>
```
#### 2 index.md 
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
