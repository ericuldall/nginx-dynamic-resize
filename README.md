# Nginx Dynamic Resize

> Ain't nobody got time for that...
____________________________________

I was recently migrating one of our server to a new cloud provider and started optimizing our static image serving method.
I noticed the original devloper of the site was using a php script to resize images before serving them... (－‸ლ)
So not only did the original request get rewritten _FROM_ www.mysite.com/img/300/path/to/my/img _TO_ www.mysite.com/images.php?width=300&file=/path/to/my/img
but we also had to deal with the overhead of php processing these images. Long story short... it was slooooooowww...wwwww...ww.w...w

Enter ``Nginx`` ✌

Using a simple set of location rules I was able to keep our current image urls (seo win!) and lose the overhead of the bulky php processing while leverging nginx's natural talent
for serving static files (sysadmin win!)

## Dependencies
1. Nginx ```apt-get install nginx``` ```yum install nginx``` ```brew install nginx (probably..hopefully)``` or download at http://nginx.org/en/download.html
2. Be enabled with the ```--with-http_image_filter_module``` - http://nginx.org/en/docs/http/ngx_http_image_filter_module.html

###### *Cheat codes for apt-get users*
I was able to install everything necessary in one line with ```apt-get install nginx-extras```

## Usage
Just call your images like this now: ```http://www.mysite.com/img/300/images/logos/site-logo.jpg```
That would serve */images/logos/site-logo.jpg* with a max-width of 300px, no upsizing will occur.

## Caveats
1. If images are larger than the *image_filter_buffer*, nginx will automatically throw a 415 Unsupported Media Type error (get used to that one)
2. ```alias``` doesn't seem to like file names with spaces in them, I'm also getting 415 in that instance (let me know if you guys have a fix for that, still banging my head against the keyboard lkajlsdfk)

### Enjoy!
