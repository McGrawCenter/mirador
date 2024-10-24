---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
---
<div id="mirador"></div>


<script>

var getvars = [];
window.location.href.replace(/[?&]+([^=&]+)=([^&]*)/gi,function(a,name,value){getvars[name]=value;});

const config = {
     id: 'mirador'
}





   if(typeof getvars['manifest'] !== 'undefined') {
   
	    	const vault = new IIIFVault.Vault();
	    	vault.loadManifest(getvars['manifest']).then(async (manifest) => {

		  switch(manifest['type']) {
		    case 'Manifest':
			    if(typeof getvars['view'] !== 'undefined') {
			      config['windows'] = [{manifestId: getvars['manifest'], view: getvars['view']}];
			    }
			    else if(typeof getvars['canvas'] !== 'undefined') {
			      config['windows'] = [{manifestId: getvars['manifest'], 'canvasIndex': getvars['canvas']}];
			    }
			    else {
			      config['windows'] = [{manifestId: getvars['manifest']}];
			    }
		    break;
		    case 'Collection':
			    if(typeof getvars['catalog'] !== 'undefined') {
			    console.log('here');
			    	config['windows'] = [];
				config['catalog'] = [];

				for(var x=0;x<manifest.items.length;x++) {
				  var url = manifest.items[x]['id'];
				  if(x <= 1) { config['windows'].push({"manifestId": url}); }
				   config['catalog'].push({"manifestId": url });
				}
			    }
			    else {
			      config['windows'] = [{manifestId: getvars['manifest']}];
			    }
		    
		    break;
		  }


	        })
	        .then((data) => {
	        console.log(config);
			Mirador.viewer(config);
	        });  
   

   
   }



</script>




