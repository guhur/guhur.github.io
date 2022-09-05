# Bootstrap

## Présentation de Bootstrap

- front-end framwork
- HTML/CSS/JS templates
- responsive design




## [Premier exemple](https://codepen.io/guhur-the-sans/pen/OJyJzRe)

Zoom sur :

```html
<meta name="viewport" content="width=device-width, initial-scale=1">
```

## Les containers

### Fluide ou pas fluide
```
<div class=".container">With container</div>
<div class=".container-fluid">With container-fluid</div>
```

### Responsive

```
<div class=".container-sm">A small container</div>
<div class=".container-md">A medium container</div>
<div class=".container-lg">A large container</div>
<div class=".container-xl">An extra large container</div>
```

## Grid

```html

<!-- Control the column width, and how they should appear on different devices -->
<div class="row">
  <div class="col-*-*"></div>
  <div class="col-*-*"></div>
</div>
<div class="row">
  <div class="col-*-*"></div>
  <div class="col-*-*"></div>
  <div class="col-*-*"></div>
</div>

<!-- Or let Bootstrap automatically handle the layout -->
<div class="row">
  <div class="col"></div>
  <div class="col"></div>
  <div class="col"></div>
</div>

```

## Exercice

Reproduire l'exemple : 
https://getbootstrap.com/docs/4.4/examples/pricing/

