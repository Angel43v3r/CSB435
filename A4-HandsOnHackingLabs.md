# Assignment 4: Hands-On Hacking Labs

# Raw Observations Section

## Google Guyere
#### Link: https://google-gruyere.appspot.com/

### Tests
1. Signed up for account, found lots of vulnerabilities.
- no username and password size minimum or restrictions.
2. Tried SQL injection when signing in but did not work.
- `‘ OR ‘1’ = ‘1` failed
3. Tried to manipulate html in new snippets and it worked
- I tried to change the html style, was able to use bold and change font size. I was also able to add a link.
    - `Hello everyone! How is your day going? <b> Enjoy the sunshine! </b>`
    - `<h1>WARNING Heading</h1>`
    - `<div style="background:yellow; padding:20px;">HTML Injection Test</div>`
    - `<img src="https://gratisography.com/wp-content/uploads/2024/10/gratisography-birthday-dog-sunglasses-1036x780.jpg">`
    - `<a href="https://www.wikipedia.org/">Click this Link</a>`
- This did not work:
    - `<style>body{background:red;}</style>`

4. I tried to do cross-site-scripts and it worked so JavaScript injection work
- I tried multiple different ones and they all worked:
    - `<script>alert(1)</script>`
    - `<a href="javascript:alert(1)">Click me</a>`
    - `<body onload=alert(1)>`
    - `<audio src/onerror=alert(1)>`
    - `<xss id=x onbeforematch=alert(1) hidden=until-found>`
    - `<img src=x onerror=alert(1)>`
    -`<script>windows.location='https://www.wikipedia.org'</script>`
    -`<xss onfocus=alert(1) autofocus tabindex=1>`
- This also fired when I delete it (click X)

### Successful Exploit
#### 1. HTML Injection

```html
<div style="background:yellow; padding:20px;">HTML Injection Test</div>
```

```html
<img src="https://gratisography.com/wp-content/uploads/2024/10/gratisography-birthday-dog-sunglasses-1036x780.jpg">
```

```html
<a href="https://www.wikipedia.org/">Click this Link</a>
```

- The website says it only accepted limited HTML like `<b>` or `<i>`, but I was able to change styling, add image, and even add links. 

#### 2. JavaScript Injection/ Cross-Site Scripting (XSS)
```
<script>alert(1)</script>
```

```
<a href="javascript:alert(1)">Click me</a>
```

```
<body onload=alert(1)>
```

```
<audio src/onerror=alert(1)>
```

```
<xss id=x onbeforematch=alert(1) hidden=until-found>
```

```
<img src=x onerror=alert(1)>
```

```
<script>windows.location='https://www.wikipedia.org'</script>
```

```
<xss onfocus=alert(1) autofocus tabindex=1>
```

- All kind of cross-site scripting or javascript injection worked and I tried different ones and they all showed the pop up.

#### 3. Sign up not very secure. 
- The password and the username does not have much restriction. It allowed weak usernames and passwords without any strong validation requirements. This can make the application vulnerable to brute force attacks.


### Failed Attempt
- SQL Injection did not work
- This css injection did not work: `<style>body{background:red;}</style>`


## CTF Learn
#### Link: https://ctflearn.com

### Challenge 88
- It was confusing how to start at first, there were no direction on what to do or how to do it. I clicked the link for the Challenge and it just showed me a simple UI with a Input where you enter text so I figured that where you enter the code. When I enter ``SELECT * FROM users where name = ''` or `SELECT * FROM users where name = '' ' OR '1'='1'` the output keep returning 0 result so I thought it was broken, but then I tried `' OR '1'='1` and it gave me output
- Another confusing was the Flag submit, I submitted `' OR '1'='1` but it says incorrect, so I went and look at the data again then i saw this `fl4g__giv3r Data: CTFlearn{th4t_is_why_you_n33d_to_sanitiz3_inputs}`, so I entered it then i solve it.


## OverTheWire - Bandit
#### Link: https://overthewire.org/wargames/ 

### Bandit Level 0
Instruction: The goal of this level is for you to log into the game using SSH. The host to which you need to connect is bandit.labs.overthewire.org, on port 2220. The username is bandit0 and the password is bandit0. Once logged in, go to the Level 1 page to find out how to beat Level 1.

Commands you may need to solve this level
ssh

#### Level 0 Tests
- I opened my windows powershell and tried to connect with SSH. 
- I tried `ssh bandit.labs.overthewire.org` and it didn't let me in, says Im trying to log in port 22 and it's not the write port. 
- I realized I didn't use the port so I tried `ssh bandit.labs.overthewire.org -p 2220`, this time I was able to log in but it used my usernmae jovy@bandit.labs.loverthewire, when I entered the `bandit0` passoword I got an error that im using the wrong username so I exited.
- I tried ` ssh bandit0@bandit.labs.overthewire.org -p 2220` and entered the password `bandit0` and I was able to connect to the server


### Bandit Level 1
Instruction: The password for the next level is stored in a file called readme located in the home directory. Use this password to log into bandit1 using SSH. Whenever you find a password for a level, use SSH (on port 2220) to log into that level and continue the game.

Commands you may need to solve this level
ls , cd , cat , file , du , find


#### Level 1 Tests
- I first entered `ls` in the powershell command line to list the files and it showed me the `readme`. 
- Now I know the readme is in this folder but not sure if its another folder or file, so I entered `cd readme` next and it output `-bash: cd: readme: Not a directory`, so now I know its not a direcgtory and that the file is in the current directory.
- Next, I need to access the file to get the password, so I use `cat readme` to read the file and I was able to read the file and get the password for Level 2.
```
Congratulations on your first steps into the bandit game!!
Please make sure you have read the rules at https://overthewire.org/rules/
If you are following a course, workshop, walkthrough or other educational activity,
please inform the instructor about the rules as well and encourage them to
contribute to the OverTheWire community so we can keep these games free!

The password you are looking for is: ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If
```

### Bandit Level 2
Instruction: The password for the next level is stored in a file called - located in the home directory

Commands you may need to solve this level
ls , cd , cat , file , du , find

#### Level 2 Tests
- I connect with `ssh bandit1@bandit.labs.overthewire.org -p2220`
- I entered the password `ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If`
- Once I logged in, I entered `ls` to list the folders and I saw `-`
- I entered `cat ./-` to read the file and I got the password for level 3 `263JGJPfgU6LtdEvgfWU1XP5yac29mFx`


### Bandit Level 3
Instruction: The password for the next level is stored in a file called --spaces in this filename-- located in the home directory

Commands you may need to solve this level
ls , cd , cat , file , du , find


#### Level 3 Tests
- I connect with `ssh bandit2@bandit.labs.overthewire.org -p2220`
- I entered teh password `263JGJPfgU6LtdEvgfWU1XP5yac29mFx`
- Once I logged in, I entered `ls` and output `--spaces in this filename--`
- I tried `cat --\ spaces\ in\ this\ filename\ --` and it did not work
- I tried `cat --spaces\ in\ this\ filename--` and it did not work
- I tried `cat ./"--spaces in this filename--"` and it worked I got `MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx` for Level 4.


## OverTheWire - Natas
#### Link: https://overthewire.org/wargames/ 

### Natas Level 0
Instruction:
```
Username: natas0
Password: natas0
URL:      http://natas0.natas.labs.overthewire.org
```

#### Level 0 Tests
- I navigate to the provided URL `http://natas0.natas.labs.overthewire.org` and entered the  username `natas0` and password `natas0`
- I got in the website and the website displayed **"You can find the password for the next level on this page."**
- Since it says I can find it on this page I viewed the page source by right clicking on the page and sure enough the password was written there for natas1, `0nzCigAq7t2iALyvU9xcHlYN4MlkIwlq`.

### Natas Level 1
Instruction:
```
Username: natas1
URL:      http://natas1.natas.labs.overthewire.org
```

#### Level 1 Tests
- I navigate to the provided URL `http://natas1.natas.labs.overthewire.org` and entered the username `natas1` and password `0nzCigAq7t2iALyvU9xcHlYN4MlkIwlq`
- I got in the website and the website displayed **"You can find the password for the next level on this page, but rightclicking has been blocked!"**
- Since right clicking is block, I needed another way to view the page source so I just typed it in the URL `view-source:http://natas1.natas.labs.overthewire.org` and it took me to the page source. I found the password for natas2 `TguMNxKo1DSa1tujBLuZJnDUlCcUAPlI`

### Natas Level 2
Instruction:
```
Username: natas2
URL:      http://natas2.natas.labs.overthewire.org
```

#### Level 2 Tests
- I navigate to the provided URL `http://natas2.natas.labs.overthewire.org` and entered the username `natas2` and password `TguMNxKo1DSa1tujBLuZJnDUlCcUAPlI`
- I got in the website and the website displayed **"There is nothing on this page "**
- I tried `view-source:http://natas2.natas.labs.overthewire.org/` but I didn't see the password in the page source.
- However in the page source I saw an img `<img src="files/pixel.png">` and clicked the image and it gave me a black background page with URL `http://natas2.natas.labs.overthewire.org/files/users.txt`. 
- Well atleast I know theres an endpoint /files so I decided to enter in the URL `http://natas2.natas.labs.overthewire.org/files/` and it took me to the files endpoint and saw that there is a `users.txt` and I clicked it and found the password for Level 3 `natas3:3gqisGdR0pjm6tpkDKdIWO2hSvchLeYH`


### Natas Level 3
Instruction:
```
Username: natas3
URL:      http://natas3.natas.labs.overthewire.org
```

#### Level 3 Tests
- I navigate to the provided URL `http://natas3.natas.labs.overthewire.org` and entered username `natas3` and password `3gqisGdR0pjm6tpkDKdIWO2hSvchLeYH`
- I got in the website and the website displayed **"There is nothing on this page "**
- I viewed the page source by right clicking on the page and I did not find it the password written there and it says **"No more information leaks!! Not even Google will find it this time"**
- I tried to type in URL `http://natas3.natas.labs.overthewire.org/files`, `http://natas3.natas.labs.overthewire.org/users.txt`, `http://natas3.natas.labs.overthewire.org/users`, `http://natas3.natas.labs.overthewire.org/password`, and `http://natas3.natas.labs.overthewire.org/password.txt` with no luck
- I run out of ideas so I searched in google "Not even Google will find it this time", then I saw a bunch of post pretty much about Natas3 and hints to use robots.txt so I did `http://natas3.natas.labs.overthewire.org/robots.txt` and saw this:
```
User-agent: *
Disallow: /s3cr3t/
```
- it looks like theres an endpooint /s3cr3t/ so I typed `http://natas3.natas.labs.overthewire.org/s3cr3t/` in the URL and found the users.txt file, I clicked it and found `natas4:QryZXc2e0zahULdHrtHxzyYkj59kUxLQ` for Level 4.




# Summary Section

## Which labs did you test?
- I tested Google Guyere, CTF Learn, OverTheWire Bandit, and OverTheWire Natas.

## For each lab, include at least one screenshot of a successful exploit beyond level 2
Include the URL in the screenshot or caption

### Google Guyere Screenshot
![Google Guyere 1]()
![Google Guyere 2]()

### CTF Learn Screenshot
![CTF Learn]()

### OverTheWire Bandit Screenshot
![OverTheWire Bandit]()

### OverTheWire Natas Screenshot
![OverTheWire Natas]()

## Which was your favourite penetration lab or testing target?
- I really like the OverTheWire Bandit and and Natas especially the level 3.

## What did you like about it?
- It was challenging and harder to crack.

## Based on this experience, for future projects you work on, what security issues will you now be more aware of?
- I will be aware of HTML exploits, authentication, SSH exploits, and HTML injections.

## What coding or configuration practices have you identified to reduce risk from the sorts of attacks you practised in these labs?
- Do not put password in HTML that can be viewed in source page. 
- Do not put password in files. 
- Do not use robots.txt
- Proper Authorization and Authentication
- Safe handling for filenames
- Maybe using CORS
- Make sure to add prevention for HTML injections.