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
     var parser = new Parser();
     parser.parse(getvars['manifest']).then((manifest)=>{
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
                    } else if (typeof getvars['target'] !== 'undefined') {
                        config['windows'] = [{
                            'manifestId': getvars['manifest'],
                            'canvasIndex': target
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
			
			config['catalog'] = [];
			config['windows'] = [];
			
			if(getvars['catalog'] == 'true') { 
			  config['windows'].push({"manifestId":'https://etcpanel.princeton.edu/IIIF/manifests/instructions/manifest.json'});
			}
			else {
			  var catalog_window_array = getvars['catalog'].split(',');
			  for (const num of catalog_window_array) {
			     config['windows'].push({"manifestId": manifest.items[num].id });
			  }
			}
			
                        manifest.items.forEach((item, index) => {
                            config['catalog'].push({
                                "manifestId": item.id
                            });
                        }); 

                    } else {
                        config['catalog'] = [];
                        config['windows'] = [];
                        if (typeof getvars['target'] !== 'undefined') { 
                           var target = getvars['target'].split('.');
                           if(target.length > 0) {
                             if(target.length == 1) { 
                               config['windows'].push({"manifestId":manifest.items[target[0]].id});
                              }
                             else if(target.length > 1) { 
                               config['windows'].push({"manifestId":manifest.items[target[0]].id, 'canvasIndex': target[1]});
                              }
                           }
                           
                        } else {
                           config['windows'].push({"manifestId":'https://etcpanel.princeton.edu/IIIF/manifests/instructions/manifest.json'});
                        }

                        
                        

                        manifest.items.forEach((item, index) => {
                            config['catalog'].push({
                                "manifestId": item.id
                            });
                        });                         
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
