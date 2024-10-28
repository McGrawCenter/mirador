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

    const vault = new IIIFVault.Vault();
    vault.loadManifest(getvars['manifest']).then(async (manifest) => {


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
                    break;
                case 'Collection':
                    if (typeof getvars['catalog'] !== 'undefined') {
			
			if(getvars['catalog'] == 'true') { getvars['catalog'] = 1; }
			var catalog_window_array = getvars['catalog'].split(',');

                        config['windows'] = [];
                        config['catalog'] = [];
                        
                        catalog_window_array.forEach((index) => {
                           var url = manifest.items[index].id;
                           config['windows'].push({
                               "manifestId": url
                           });
                        }); 
                        
                        manifest.items.forEach((item) => {
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


        })
        .then((data) => {
            Mirador.viewer(config);
            console.log(Mirador.viewer);
        });



} else {
    Mirador.viewer(config);
}


/*

  "viewers": {
    "window-9bfc84e3-cda3-47a9-b72c-38042d0e8625": {
      "flip": false,
      "rotation": 0,
      "x": 643,
      "y": 619,
      "zoom": 0.000617283950617284
    }
  },
*/

</script>




