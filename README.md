﻿# inWidget Proxified - free Instagram widget for your website


# net::ERR_BLOCKED_BY_RESPONSE issue (new in 2021)
Instagram has just updated cross-origin policy on their images, so web browsers now throw ERR_BLOCKED_BY_RESPONSE in console and refuse to display the images.
To mitigate this, the inwidget has been updated to proxy images via simple image proxy.
https://github.com/restyler/inwidget-proxified/blob/master/imgproxy.php

(consider switching to nginx/cloudflare proxying for better performance and cache support)


----------

# Commercial support and custom development
Please contact http://t.me/sergeyvvv5

----------


This library is based on PHP and allows you to show photos from an Instagram account or hashtag on your website, without Instagram Developer account or Instagram API access. This fork also does not require your Instagram login and password.

## This is a proxified fork of an archived project https://github.com/aik27/inwidget , and this fork tries to solve the main issue of the parent project - reliable access to Instagram from datacenter ip ranges, without getting banned with 429 and 302 errors (e.g. see  https://github.com/aik27/inwidget/issues/29 ).
This fork uses RapidAPI solution under the hood (which works much better than just using residential proxies), this requires subscription but Free plan is more than enough for 1 widget. It does not require your instagram login or password anymore!
Get your subscription key here: https://rapidapi.com/restyler/api/instagram40 and put to it config.php


[Demonstration >>](https://inwidget.apiroad.net/)

![demo](https://inwidget.apiroad.net/img2.png?1)

### Features:

+ Many settings
+ Direct links to photos
+ Profile stats
+ Adaptive, responsive template
+ Support of several hashtags
+ Language auto detection
+ Works without ACCESS_TOKEN
+ Inserting with one line in HTML
+ Many skins
+ Without advertising
+ For any use
+ Detailed instructions

## System requirements

PHP >= 5.4.0 with cURL extension

## Installation


### 1. Upload source code of the widget to the public folder of your website

[Download](https://github.com/restyler/inwidget-proxified/releases) latest release source code. Extract /inwidget folder.
Upload /inwidget folder to website with all files inside.

Your files structure should look like this be:
 - index.php (your website main PHP file)
 - inwidget/ (widget code)
 - inwidget/index.php (inwidget files are located here)

**Note**. inWidget uses relative paths, so you can upload it to any folder. After that do not forget change URL in IFRAME tag.

### 2. Set write permissions to the cache folder 

inWidget stores cached data in /inwidget/cache folder (if you downloaded the repo and extracted it to /inwidget)
If this directory does not have write permissions you will see ERROR #101.
In case you are using Apache:
```sh
chown www-data inwidget/cache
```


### 3. Configuration

Modify /inwidget/config.php
You will need to specify Instagram login and other params

List of parameters:

+ **LOGIN** - Instagram login
+ **HASHTAG** - hashtags separated by a comma (for example: girl, man). Selection will be made from around the world in the order that photos were marked with desired tags
+ **RAPIDAPI_KEY** - RapidAPI key, required. Retrieve your key on https://rapidapi.com/restyler/api/instagram40 (Free plan should be more than enough for responsible use with 12h cache)
+ **ACCESS_TOKEN** - **DEPRECATED, do not use this in 2021!** a hashkey granted to you by an Instagram app. 
+ **authLogin and authPassword** - **DEPRECATED, do not use this in 2021!** login and password of an account for authorization. This options are NOT required. Authorization is necessary for alternative methods of obtaining data and provides more stability when you using the undocumented API. I advise you to create a separate account for this with disabled two-step authentication. Authorization data is not transferred to third parties and author of the widget
+ **loginAvailable** - If you need to separate logins on diffent website pages, just add possible logins to the array below. After that you can send login to the widget by GET variable. It workds only with the undocumented API. Example: /inwidget/index.php?login=fotokto_ru
+ **tagsAvailable** - Same option for tagged media. Add possible tags to the array below. Then you can use GET variable for tags. Example: /inwidget/index.php?tag=photography. You can mix this option with "loginAvailable" and "tagsFromAccountOnly"
+ **tagsBannedLogins** - Specify here list of banned logins. Photos of these users will not be display in the widget. Separate usernames by a comma. For example: mark18, kitty45
+ **tagsFromAccountOnly** - Search tagged media from your account only [ true / false ]. To improve search increase value of "imgCount" option
+ **imgRandom** - Random order of pictures [ true / false ]
+ **imgCount** - How many pictures the widget will get from Instagram?
+ **cacheExpiration** - Cache expiration time (hours)
+ **cacheSkip** - Skip cache data [ true / false ]. So mean, requests to Instagram API will be sending every time. Warning! Use true value only for debug
+ **cachePath** - Full path to the cache directory
+ **skinDefault** -  Default skin. Possible values: *default, modern-blue, modern-green, modern-red, modern-orange, modern-grey, modern-black, modern-violet, modern-yellow*. This option may no effect if you set a skin by $_GET variable
+ **skinPath** - Path to the skins directory
+ **langDefault** - Default language [ ru / en / ua ] or something else from the langs directory
+ **langPath** - Full path to the langs directory
+ **langAuto** - Language auto-detection [ true / false ]. This option may no effect if you set a language by $_GET variable

### 4. Paste this code into your html template

```
<!-- default -->
<iframe src='/inwidget/index.php' scrolling='no' frameborder='no' style='border:none;width:260px;height:330px;overflow:hidden;'></iframe> 
```

Or use another examples with different display type:

```
<!-- Without profile -->
<iframe src='/inwidget/index.php?toolbar=false&color=3423c1' data-inwidget scrolling='no' frameborder='no' style='border:none;width:260px;height:320px;overflow:hidden;'></iframe>

<!-- Mini 1 -->
<iframe src='/inwidget/index.php?width=100&inline=2&view=12&toolbar=false' data-inwidget scrolling='no' frameborder='no' style='border:none;width:100px;height:320px;overflow:hidden;'></iframe>

<!-- Mini 2 -->
<iframe src='/inwidget/index.php?width=100&inline=1&view=3&toolbar=false' data-inwidget scrolling='no' frameborder='no' style='border:none;width:100px;height:320px;overflow:hidden;'></iframe>

<!-- Horizontal orientation -->
<iframe src='/inwidget/index.php?width=800&inline=7&view=14&toolbar=false' data-inwidget scrolling='no' frameborder='no' style='border:none;width:800px;height:295px;overflow:hidden;'></iframe>

<!-- Large previews -->
<iframe src='/inwidget/index.php?width=800&inline=3&view=9&toolbar=false&preview=large' data-inwidget scrolling='no' frameborder='no' style='border:none;width:800px;height:850px;overflow:hidden;'></iframe> 
```

## Fine-tune widget display

Parameters are passed as GET variables when accessing to the widget script. For that you must change the URL in IFRAME tag. For example, to set the widget width to 600px and display five photos per a single row, you need to add appropriate parameters in the URL.

```
/inwidget/index.php?width=600&inline=5
```

List of GET parameters:

+ **color** - primary color of the widget, in hex format, without '#' symbol, e.g. `3423c1`
+ **width** -  the widget width (default: 260px)
+ **inline** - number of photos per line (default: 4 pcs.)
+ **view** - how many photos can be displayed in the widget (default: 12 pcs, max.: 30 pcs, you can change it in config.php)
+ **toolbar** - display toolbar with avatar and statistics ( true / false, default: true)
+ **preview** - size and quality of images (small - 320px, large - 640px, fullsize - maximum avalible size, default: large)
+ **lang** - the widget language (ru / en / ua, default settings are taken from config.php ). Priority of this parameter is higher than for settings in config.php
+ **skin** - the widget skin (default / modern-blue / modern-green / modern-red / modern-orange / modern-gray / modern-black / modern-violet / modern-yellow). Default value: default. Priority of this parameter is higher than for settings in config.php
+ **adaptive** - adaptive, responsive mode (true / false, by default: false). Widget will automatically adjust to dimensions of html container or browser window

When you changing width or number of photos, do not forget to change IFRAME tag size.


## How to make the widget adaptive / responsive? [(example)](https://inwidget.ru/adaptive.php)

Add GET variable "adaptive" in the URL of IFRAME tag.
 
```
/inwidget/index.php?adaptive=true
```

The value must be set to true. After that, the widget will automatically adjust to the dimensions of html container or browser window. In this case, the GET parameter "width" will be ignored, the "inline" parameter will have an effect when the widget width of more than 400px.

Please, see demonstration of adaptive mode: https://inwidget.ru/adaptive.php


## For developers

You can include inWidget library in your application and set parameters through the class constructor. Be careful with the file paths when using example below. The classes support autoloading.

By default the widget use undocumented API that provided by [instagram-php-scraper](https://github.com/postaddictme/instagram-php-scraper) library. To switch to the endpoint API, you need to specify ACCESS_TOKEN.

```php
#require_once 'inwidget/classes/Autoload.php';
require_once 'inwidget/classes/InstagramScraper.php';
require_once 'inwidget/classes/Unirest.php';
require_once 'inwidget/classes/InWidget.php';

try {
	
    // Options may change through the class constructor. For example:
    
    $config = array(
       'LOGIN' => 'fotokto_ru',
       'HASHTAG' => '',
       'ACCESS_TOKEN' => '',
       'authLogin' => '',
       'authPassword' => '',
       'tagsBannedLogins' => '',
       'tagsFromAccountOnly' => false,
       'imgRandom' => true,
       'imgCount' => 30,
       'cacheExpiration' => 6,
       'cacheSkip' => false,
       'cachePath' =>  $_SERVER['DOCUMENT_ROOT'].'/inwidget/cache/',
       'skinDefault' => 'default',
       'skinPath'=> '/inwidget/skins/',
       'langDefault' => 'ru',
       'langAuto' => false,
       'langPath' => $_SERVER['DOCUMENT_ROOT'].'/inwidget/langs/',
    );
    
    $inWidget = new \InWidget\Core($config);
	
    // Also, you may change default values of properties

    /*
    $inWidget->width = 800;         // widget width in pixels
    $inWidget->inline = 6;          // number of images in single line
    $inWidget->view = 18;	        // number of images in widget
    $inWidget->toolbar = false;     // show profile avatar, statistic and action button
    $inWidget->preview = 'large';   // quality of images: small, large, fullsize
    $inWidget->adaptive = false;    // enable adaptive mode
    $inWidget->skipGET = true;      // skip GET variables to avoid name conflicts
    $inWidget->setOptions();        // apply new values
    */
	
    $inWidget->getData();
    include 'inwidget/template.php';

}
catch (\Exception $e) {
    echo $e->getMessage();
}
```

## Error codes

**ERROR #101** - can not access to the cached file. You need to change permissions for directory: /inwidget/cache 

If cached file does not exist, the widget will try to create it. Then the widget will try to open it for reading and writing. Incorrect rights provide this error. If you already had some files in the cache directory, just delete them, because they also may has incorrect rights.

**ERROR #102** - can not get the last modification time of the cached file.

Perhaps, this function is limited or not supported by your server's file system. If the widget can not determine the time, cache will always be irrelevant, which will result in permanent requests to Instagram API.

**ERROR #500** - unknown error

Please, see what exactly was written into the cached file. This error is generated by the official API or instagram-php-scraper library. In most cases, it means a problem when sending or receiving data from Instagram server. Delete the cached file and refresh a page (on which the widget is displayed) to try send request again.

## Feedback, questions and suggestions

+ Visit website: https://inwidget.apiroad.net


## Copyrights of original repo 

+ Author: Alexandr Kazarmshchikov
+ E-mail: aik@inwidget.ru
+ Site: https://inwidget.ru

## License

This library is free software; you can redistribute it and/or modify it under the terms of MIT license: https://inwidget.ru/MIT-license.txt
