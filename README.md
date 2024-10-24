# Mirador
Mirador 3 in a Jekyll site

https://mcgrawcenter.github.io/mirador/

## Options
### Manifests

#### ?manifest=

A single IIIF manifest can be loaded into the viewer by adding a 'manifest' parameter to the URL, such as:

https://mcgrawcenter.github.io/mirador/?manifest=https://figgy.princeton.edu/concern/scanned_resources/65889df9-628c-4162-8430-b7ade1d1fe21/manifest

#### ?manifest=...&view=gallery
Load the manifest in gallery view

#### ?manifest=...&canvas=5
Load the manifest with the 5th canvas displayed by default. Note: the first canvas is number 0

### Collections

#### ?manifest=...&catalog=1
If a collection manifest is loaded with the manifest URL parameter, you optionally may also add 'catalog=1' to load each manifest individually.

https://mcgrawcenter.github.io/mirador/?manifest=https://iiif.library.ucla.edu/collections/ark%3A%2F21198%2Fz1vb25zg&catalog=true



