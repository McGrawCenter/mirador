---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
---
<div id="mirador-viewer"></div>

<script src="{{ "assets/js/mirador3.min.js" | relative_url }}"></script>


<script type="text/javascript">

var config = {id:"mirador"}
Mirador.viewer(config);

</script>


