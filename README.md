# Make-SEO-Friendly-Clean-Url-in-PHP-using-.htaccess

In this tutorial you will learn how to make seo friendly url in PHP using .htaccess file. User Friendly Url is one of the required things for Content Marketing. With the help of pretty url your website content will be listed on search engine very fast. Clean Url is one part of Search Engine Optimization. SEO Friendly Url  will increase our ranking on different search engine.

### Result

```php
Old URL - https://www.domain.com/post.php?post_url=this-is-a-test-message
New URL - https://www.domain.com/post/this-is-a-test-message
```

### Table Structure
```sql
CREATE TABLE IF NOT EXISTS `tbl_post` (  
  `post_id` int(11) NOT NULL AUTO_INCREMENT,  
  `post_title` text NOT NULL,  
  `post_text` text NOT NULL,  
  `post_url` text NOT NULL,  
  PRIMARY KEY (`post_id`)  
 ) ENGINE=MyISAM DEFAULT CHARSET=latin1 AUTO_INCREMENT=1 ;  
 ```
### index.php
```php
<?php  
 $connect = mysqli_connect("localhost", "root", "", "test_db");  
 if(isset($_POST["submit_btn"]))  
 {  
      $post_title = mysqli_real_escape_string($connect, $_POST["post_title"]);  
      $post_text = mysqli_real_escape_string($connect, $_POST["post_text"]);  
      $post_title = htmlentities($post_title);  
      $post_text = htmlentities($post_text);  
      $sql = "INSERT INTO tbl_post (post_title, post_text, post_url) VALUES ('".$post_title."', '".$post_text."','".php_slug($post_title)."')";  
      if(mysqli_query($connect, $sql))  
      {  
           header("location:post/".php_slug($post_title)."");  
      }  
 }  
 function php_slug($string)  
 {  
      $slug = preg_replace('/[^a-z0-9-]+/', '-', trim(strtolower($string)));  
      return $slug;  
 }  
 ?>  
 <html>  
      <head>  
           <title>Make SEO Friendly / Clean Url in PHP using .htaccess</title>  
           <style>  
           .container  
           {  
                width:700px;  
                margin:0 auto;  
                border:1px solid #ccc;  
                padding:16px;  
           }  
           .form_text  
           {  
                width:100%;  
                padding:6px;  
           }  
           </style>  
      </head>  
      <body>  
           <div class="container">  
                <h3 align="center">How to Make SEO Friendly / Clean Url in PHP using .htaccess</h3>  
                <form name="submit_form" method="post">  
                     <p>Post Title  
                     <input type="text" name="post_title" class="form_text"/>  
                     </p>  
                     <p>Post Text  
                     <textarea name="post_text" class="form_text" rows="5"></textarea>  
                     </p>  
                     <p><input type="submit" name="submit_btn" value="Submit" />  
                </form>  
           </div>  
      </body>  
 </html>
 ```
### post.php

```php
<?php  
 $connect = mysqli_connect("localhost", "root", "", "test_db");  
 $post_url = $_GET["post_url"];  
 $sql = "SELECT * FROM tbl_post WHERE post_url = '".$post_url."'";  
 $result = mysqli_query($connect, $sql);  
 ?>  
 <html>  
      <head>  
           <title>Make SEO Friendly / Clean Url in PHP using .htaccess</title>  
           <style>  
           .container  
           {  
                width:700px;  
                margin:0 auto;  
                border:1px solid #ccc;  
                padding:16px;  
           }  
           .form_text  
           {  
                width:100%;  
                padding:6px;  
           }  
           </style>  
      </head>  
      <body>  
           <div class="container">  
                <h3 align="center">Make SEO Friendly / Clean Url in PHP using .htaccess</h3>  
                <?php  
                if(mysqli_num_rows($result) > 0)  
                {  
                     while($row = mysqli_fetch_array($result))  
                     {  
                          echo '<h3>'.$row["post_title"].'</h3>';  
                          echo '<p>'.$row["post_text"].'</p>';  
                     }  
                }  
                else  
                {  
                     echo '404 Page';  
                }  
                ?>  
           </div>  
      </body>  
 </html>  
 ```
 
### .htaccess File
```
RewriteEngine On  
RewriteRule ^post/([a-zA-Z0-9-/]+)$ post.php?post_url=$1  
RewriteRule ^post/([a-zA-Z-0-9-]+)/ post.php?post_url=$1  
```
