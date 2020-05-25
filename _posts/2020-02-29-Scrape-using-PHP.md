---
title: Scrape using PHP
date: 2020-02-29 12:28:12 -0500
categories: [Programming]
tags: [php]
---

I wrote some articles in my Wechat official account before. I worried that some day the links might not work anymore, so I decided to get the local html files of those articles. And the following is what I did. Note that I owned the Wechat official account, so there is no legal issue involved. But if you try to use the following code to scrape other Wechat official account, please keep in mind about the authorization. 

Also, Wechat would change the html format occasionally, so you might need some modification if my code doesn't work. But the general idea should be correct.

## Crawl the style, main content, and style of the link.

```php
<?php
// article_url is the url of the wechat article
$article_url = "url-of-the-article";
$html = file_get_contents($article_url);

/* ---------------  get title content ----------------- */
preg_match_all("/\"img-content\" class=\"rich_media_wrp\">(.*)<\/em>/Us", $html, $title_content);

// class='rich_media_wrp'
$title_content = "<div id='img-content'>". $title_content[1][0] . "</em> </div>";

// write to title.php file
$filename = "includes/title.php";
$file = fopen($filename, "w");
fwrite($file, $title_content);
fclose($file);


/* ---------------  get main content ----------------- */
preg_match_all("/\"js_content\" style=\"visibility: hidden;\">(.*)<\/div>/iUs",$html,$content);

$content = "<div id='js_content'>".$content[1][0] . "</div>";

// a function to get images form url
function file_get_contents_curl($url) { 
    $ch = curl_init(); 
  
    curl_setopt($ch, CURLOPT_HEADER, 0); 
    curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1); 
    curl_setopt($ch, CURLOPT_URL, $url); 
  
    $data = curl_exec($ch); 
    curl_close($ch); 
  
    return $data; 
} 

// download all of the images in this article
// search for the urls of the images
preg_match_all("/data-src=\"(.*)\" data-type=/U", $content, $imgs, PREG_PATTERN_ORDER);

$i = 1;
foreach ($imgs[1] as $url) {
    
    $img = "images/img-" . $i . ".png";  
  
    // write image into file 
    file_put_contents($img, file_get_contents_curl($url)); 

    echo "File downloaded and saved to " . $img . " !<br>";
    
    // replace the original src to the local src
    $content = str_replace($url, $img, $content);
    
    $i++;
}

// replace data-src with src to work on local html
$content = str_replace("data-src","src",$content);

// enable video and flash
$content = str_replace("preview.html","player.html",$content);

// write to content.php file
$filename = "includes/content.php";
$file = fopen($filename, "w");
fwrite($file, $content);
fclose($file);

/* ---------------  get style ----------------- */
preg_match_all("/<style>\.(.*)<\/style>/Us", $html, $style_content);

$style_content = "<style>." . $style_content[1][0] . "</style>";

$filename = "includes/style.php";
$file = fopen($filename, "w");
fwrite($file, $style_content);
fclose($file);

?>
```


## Create my own php page

```php
<html>
<head>
    <meta charset="UTF-8">
    <title>Title You Want</title>
</head>
<body>
    <?php
        require_once 'includes/style.php';
    ?>
    <?php
        require_once 'includes/title.php';
    ?>
    <?php
        require_once 'includes/content.php';
    ?>
</body>
</html>
```

Note that php is dynamic while github page supports static only, so I cannot insert php into this Jekyll blog. 
