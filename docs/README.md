---
sidebar: false
---

<Hero />

## Usage example

```html
<portal to="destination">
  <p>This slot content will be rendered wherever the
    <portal-target> with name 'destination'
    is located.
  </p>
</portal>

<portal-target name="destination">
  <!--
  This component can be located anwhere in your App
  (i.e. right before the </body> tag, for good for overlays).
  The slot content of the above portal component will be rendered here.
  -->
</portal-target>
```
