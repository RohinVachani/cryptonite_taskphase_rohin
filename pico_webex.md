# **Web Exploitation**

## **where are the robots**

This challenge provides us with a url link to a static website `http://jupiter.challenges.picoctf.org:56830`
The name of the challenge gives us an idea that we are to look for "robots". 

Search engines like Google use automated scripts or programs to browse and index webpages that are on the internet. This is done for various purposes like better the search engines and update online services. `robots.txt` are text files stored in the root directory of a website that instruct these web crawlers on how to interact with the website, such as what parts of websites the bots are allowed to crawl and index. 

When we visit the website and append the url with `/robots.txt`, we see the following text:
> User-agent: *

> Disallow: /1bb4c.html

The first component of the file `User-agent` specifies that this instruction is for all bots
THe second component of the file `Disallow` specifies that these bots are not allowed to crawl to  `http://jupiter.challenges.picoctf.org:56830/1bb4c.html`

We obtain the flag when we visit the html site.

## **inspect HTML**
Upon launching the instance we are provided with a url to a static website. When we `inspect` the website and view the source code, we can view the HTML code of the website.
HTML comments are of the form `<!-- This is an HTML comment -->` and are not displayed on the web page.
The flag is in the comment of the HTML code and we can now retreive it.

## **dont-use-client-side**
We are provided with a link to a portal. When we try to input some random credentials and verify to access this portal, we are alerted with `Incorrect Password`.

Upon viewing the source code for this website , we can find the script that is responsible for validating the credentials.
```
<script type="text/javascript">
  function verify() {
    checkpass = document.getElementById("pass").value;
    split = 4;
    if (checkpass.substring(0, split) == 'pico') {
      if (checkpass.substring(split*6, split*7) == 'a3c8') {
        if (checkpass.substring(split, split*2) == 'CTF{') {
         if (checkpass.substring(split*4, split*5) == 'ts_p') {
          if (checkpass.substring(split*3, split*4) == 'lien') {
            if (checkpass.substring(split*5, split*6) == 'lz_1') {
              if (checkpass.substring(split*2, split*3) == 'no_c') {
                if (checkpass.substring(split*7, split*8) == '9}') {
                  alert("Password Verified")
                  }
                }
              }
      
            }
          }
        }
      }
    }
    else {
      alert("Incorrect password");
    }
    
  }
</script>
```

Piecing the fragments together we obtain the flag!

## **Power Cookie**

This challenge is related to website cookies. Website cookies are text file that are stored on user's device thorugh the web browser. They contain information about users for Authentication, Personalisation, Analytics and Advertising

We are yet again provided with a website link. When we visit the site and click on the button `Continue as guest` , we are told that there are no guest services.
Inspect the website and navigate to the `Cookies` tab.
Theres is a cookie named `Admin` whose is set to 0. Change the value to 1 and refresh to obtain the flag.

## **IntroToBurp**
For this we have to intercept the communication using BurpSuite. We have fill in some random credentials and forward the request. Do the same for OTP and remove the line where we can see our entred OTP value. This will give us the flag.

## **SQL Dierect**

Like any databse this will have relations.
I use `\d` to display the list of relations
```
        List of relations
 Schema | Name  | Type  |  Owner   
--------+-------+-------+----------
 public | flags | table | postgres
(1 row)
```

Now all we have to do is `select * from flags;` which will return all the columns from the table.
```
 id | firstname | lastname  |                address                 
----+-----------+-----------+----------------------------------------
  1 | Luke      | Skywalker | picoCTF{L3arN_S0m3_5qL_t0d4Y_31fd14c0}
  2 | Leia      | Organa    | Alderaan
  3 | Han       | Solo      | Corellia
```

























