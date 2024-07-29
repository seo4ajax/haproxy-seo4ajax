[SEO4Ajax](https://www.seo4ajax.com) is a service that allows AJAX websites
(e.g. based on Angular, React, Vue.js, Svelte, Backbone, Ember, jQuery etc.) to
be indexable by search engines and social networks.

## Integration in the configuration file

Integrate the following lines in the configuration file and deplace 
`<TOKEN_SEO4AJAX>` with the site token in SEO4Ajax (e.g. f594d3367b818ecefe28e9caba24fe16)

```
frontend my-frontend
    mode http
    bind :80
    
    acl user-agent-bot hdr_sub(User-Agent) -i baiduspider bot facebookexternalhit pinterest
    acl url-asset path_end js css xml less png jpg jpeg gif pdf doc txt ico rss zip mp3 rar exe wmv doc avi ppt mpg mpeg tif wav mov psd ai xls mp4 m4a swf dat dmg iso flv m4v torrent ttf woff
    use_backend seo4ajax if user-agent-bot !url-asset

backend seo4ajax
   mode http
   timeout server 20s
   server seo4ajax api.seo4ajax.com:443 check ssl verify none
   http-request replace-path ^/(.*) /<TOKEN_SEO4AJAX>/\1
```
