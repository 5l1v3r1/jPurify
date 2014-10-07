# jPurify

jPurify is a plugin that automatically adds XSS-safety to jQuery. The reason why we do that is jQuery's lack of DOMXSS protection. We wanted to create a jQuery plugin, that adds super-easy-to-use and fully automatic HTML sanitation to the whole jQuery API.

jPurify is maintained by the same people that look after [DOMPurify](/cure53/DOMPurify).

## What does it do?

jPurify, once included, simply overwrites some security-critical jQuery methods and adds proper HTML santitation. Let's have a look at an example to clarify:

```html
<html>
    <head>
        <script src="jquery.js"></script>
    </head>
    <body>
        <div id="html"></div>
        <script>
            // location.hash could be <svg/onload=alert(domain)>
            $('#html').html('<h1>'+location.hash+'</h1>');
        </script>
    </body>
</html>

```

This code shown above is vulnerable to XSS. An attacker can influence `location.hash` to contain evil HTML and then attack your website's users. Not nice. Now let's have a look at what jPurify accomplishes: 

```html
<html>
    <head>
        <script src="jquery.js"></script>
        
        <!-- makes the code below be secure -->
        <script src="purify.js"></script>
        <script src="jpurify.js"></script>
    </head>
    <body>
        <div id="html"></div>
        <script>
            // location.hash could be <svg/onload=alert(domain)>
            $('#html').html('<h1>'+location.hash+'</h1>');
        </script>
    </body>
</html>

```

Now, the XSS attack is being blocked. jPurify inspects and sanitizes the arguments sent to the vulnerable methods. The bad stuff is being removed, the good stuff is left intact, happy times.

## How do I use it?

It's easy. Just include DOMPurify **and** jPurify on your website. It will seemlessly plug into jQuery and sanitize any potentially dangerous DOM-transaction. 

```html
<script type="text/javascript" src="purify.js"></script>
<script type="text/javascript" src="jpurify.js"></script>
```

