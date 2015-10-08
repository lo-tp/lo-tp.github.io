Date:2015-10-08 19:32
Title:Initialize Wordpress with Docker
Author:Lotp
tags:Wordpress, Docker

This is a step by step tutorial about how to install wordpress with docker.
In this post, I'll also include some basic modification you'll need to use wordpress in China.
*********
**Update**:

There is a better way to use accomplish this target.

Check this [post][betterWay]

*********
##Install Wordpress
1.	Pull Images

	* `docker pull mysql`
	* `docker pull wordpress`

1.	Make and Run Mysql Container

	`docker run --name wordpressdb -e MYSQL_ROOT_PASSWORD=password -e MYSQL_DATABASE=wordpress -d mysql:5.7`

1.	Make and Run Worepress Container

	`docker run -e WORDPRESS_DB_PASSWORD=password -d --name wordpress --link wordpressdb:mysql -p 10.0.0.47:50002:80 -v "/home/lotp/workingSpace/blog/wordpress":/var/www/html  wordpress`

##Struggle with the Firewall
1.	Deal with Google Fonts

	Open wp-includes/script-loader.php.
	Search for fonts.googleapis.com.
	Replace **googleapis** with **useso**.

1.	Deal with Gravatar

	Add these lines to the end your *wp-includes/functions.php*

		function junzibuqi_com_gravatar( $avatar ) {
		$avatar = str_replace( array( 'http://www.gravatar.com', 'http://0.gravatar.com', 'http://1.gravatar.com', 'http://2.gravatar.com' ), 'https://secure.gravatar.com', $avatar );return $avatar;
		}
		add_filter( 'get_avatar', 'junzibuqi_com_gravatar' );
	
	Also don't forget to do some modification to *wp-settings.php*
	Reverse the order of these two lines.

		require (ABSPATH . WPINC . '/functions.php');
		require (ABSPATH . WPINC . '/plugin.php');
	
##Useful Plugin
1.	Anti Spam
	
	Captcha by BestWebSoft

##Password
TPLctdSvuM)0k$^Vau
##What You Need to Change about the Settings

1.	Help! Oops, that page can't be found error message

	`Settings -> Permalink Settings: Switched from "Day and name" to "Default"`

1.	How to Change the Line Height and Spacing

	edit `/wp-content/themes/simple-life/style.css`

		p{
			line-height: 180%;
			margin-bottom: 0.7em;
		}

[betterWay]:initialize-wordpress-with-docker-compose.html
