---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
---
<div id="mirador"></div>


<script>
var getvars = [];
window.location.href.replace(/[?&]+([^=&]+)=([^&]*)/gi, function(a, name, value) {
    getvars[name] = value;
});

const config = {
    id: 'mirador'
}


if (typeof getvars['manifest'] !== 'undefined') {

    
  var x = new SimpleParser();
  x.convert(getvars['manifest']).then((manifest)=>{
    console.log(manifest);

    switch (manifest['type']) {
                case 'Manifest':
                    if (typeof getvars['view'] !== 'undefined') {
                        config['windows'] = [{
                            'manifestId': getvars['manifest'],
                            'view': getvars['view']
                        }];
                    } else if (typeof getvars['canvasindex'] !== 'undefined') {
                        config['windows'] = [{
                            'manifestId': getvars['manifest'],
                            'canvasIndex': getvars['canvasindex']
                        }];
                    } else if (typeof getvars['canvas'] !== 'undefined') {
                        config['windows'] = [{
                            'manifestId': getvars['manifest'],
                            'canvasId': getvars['canvas']
                        }];
                    } else {
                        config['windows'] = [{
                            'manifestId': getvars['manifest']
                        }];
                    }
                    if(typeof getvars['nav'] !== 'undefined' || typeof getvars['thumbnails'] !== 'undefined') {
                        config['windows'][0].thumbnailNavigationPosition = 'far-bottom';
                        console.log(config);
                    }
                    break;
                case 'Collection':
                    if (typeof getvars['catalog'] !== 'undefined') {
			
			/*
			if(getvars['catalog'] == 'true') { getvars['catalog'] = 1; }
			var catalog_window_array = getvars['catalog'].split(',');
			*/
			

                        config['windows'] = [{"manifestId":'https://etcpanel.princeton.edu/IIIF/manifests/instructions/manifest.json'}];
                        config['catalog'] = [];
                        /*
                        manifest.items.forEach((item, index) => {
			   if(index < 1) {
                           var url = item.id;
                           config['windows'].push({
                               "manifestId": url
                           });
                           }
                        }); 
                        */
                        manifest.items.forEach((item, index) => {
                            config['catalog'].push({
                                "manifestId": item.id
                            });
                        });                       

                    } else {
                        config['windows'] = [{
                            manifestId: getvars['manifest']
                        }];
                    }

                    break;
      }
  }).then((data) => {
            Mirador.viewer(config);
            console.log(config);
  });;	




} else {
    Mirador.viewer(config);
}



</script>




