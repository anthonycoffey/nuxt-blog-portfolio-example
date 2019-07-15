---
title: "Use Regular Expressions to Prepend Strings on Paths"
date: "2019-01-19"
---

I was working on building a custom plugin for a client, and I needed to run a search/prepend style function on a block of HTML for a relative path that wasn't linking up to the plugin directory that I was working on.

So, naturally I used a regular expression to target the /assets/\* folder pattern and prepend the rest of the path, which made all the broken assets work! The battle was won, but the war was far from over.  
  
Here is the [regular expression](https://regex101.com/r/LBirPz/2) that I used. I generated the PHP code for the regular expression using an awesome online tool called [Regex101.com](https://regex101.com/)

[Click here to view the regular expression](https://regex101.com/r/LBirPz/2) that I used to prepend a path onto all images in a string of HTML.

Shown below is the PHP code that I wrote to use the regular expression with the help of [preg\_replace](http://php.net/manual/en/function.preg-replace.php) (see link for more info)

```
$regex = '/(\/assets)/';
$str = '/assets/images/image.jpg';
$subst = '/my-path$1';

$result = preg_replace($re, $subst, $str);
```

The above example would result in the following:


- *before:* /assets/images/image.jpg

- *after:* /my-path/assets/images/image.jpg


I actually even went a bit further with it by adding a callback function that can check to see if the matched pattern has a trailing slash or not. Maybe I'll share that in my next post or add it to this one later on.

Thanks for reading, if you have any questions let me know in the comments below.
