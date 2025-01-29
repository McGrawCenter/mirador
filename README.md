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

#### ?manifest=...&nav=1 OR ?manifest=...&thumbnails=1 
Load the thumbnail navigation toolbar at the bottom of the screen

#### ?manifest=...&canvasindex=5
Load the manifest with the 5th canvas displayed by default. Note: the first canvas is number 0

#### ?manifest=...&canvas=...
Load the manifest with the canvas with id indicated with the canvas parameter

### Collections

#### ?manifest=...&catalog=1
If a collection manifest is loaded with the manifest URL parameter, you optionally may also add 'catalog=1' to load each manifest individually and to load the first manifest in a window by default.

https://mcgrawcenter.github.io/mirador/?manifest=https://iiif.library.ucla.edu/collections/ark%3A%2F21198%2Fz1vb25zg&catalog=1

The catalog parameter can also be a comma separated list of manifest indexes to open by default

https://mcgrawcenter.github.io/mirador/?manifest=https://iiif.library.ucla.edu/collections/ark%3A%2F21198%2Fz1vb25zg&catalog=1,5,8
