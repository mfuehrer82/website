[![Build Status](https://travis-ci.org/php-usergroup-dresden/website.svg?branch=master)](https://travis-ci.org/php-usergroup-dresden/website)

# The PHP USERGROUP DRESDEN e.V. website

## Edit the website

The website is (obviously) generated static content.
 
If you want to make changes, fix typos or add missing content, please follow these steps.

### 1. Fork & clone the respository

* Please fork the repository to your github account.
* Clone the repository to your local machine

```bash
$ git clone https://github.com/<your-github-user>/website.git
$ cd website/
```

### 2. Install the static page generator

The static page generator is a PHAR that is installed using [composer](https://getcomposer.org) 
and [tm/tooly-composer-script](https://github.com/tommy-muehle/tooly-composer-script).

Simply run:

```bash
$ mkdir -p vendor/bin
$ composer update
```

The static page generator PHAR is placed to `vendor/bin/spg.phar` and is executable.

### 3. Make it a Document Root of a webserver

The simplest way is to use the build-in PHP webserver, like this:

```bash
$ php -S 127.0.0.1:8088
# Should print something like this
PHP 7.0.11 Development Server started at Fri Nov  4 11:03:32 2016
Listening on http://127.0.0.1:8088
Document root is /Users/hollodotme/Sites/website
Press Ctrl-C to quit.
```

### 4. Generate the pages and sitemap for your locale base URL

In order to generate the pages for your local URL (http://127.0.0.1:8088 or whatever your webserver's URL is), you need 
to run the static page generator with the option `--baseUrl="http://127.0.0.1:8088/docs"`.

```bash
$ vendor/bin/spg.phar generate:pages --baseUrl="http://127.0.0.1:8088/docs" ./Project.json
$ vendor/bin/spg.phar generate:sitemap --baseUrl="http://127.0.0.1:8088/docs" ./Project.json
```

### 5. Open in browser

Now you should be able to view the pages in your browser when visiting http://127.0.0.1:8088/docs.

### 6. Make changes

* You can edit the content files located in the `./contents` directory.
* Please **do not edit** the `.html` files, those changes will be gone when generating the pages.
* You can add new images in `doc/images/`
* You can add new downloads in `doc/downloads/`
* You can add new pages in the `./Project.json` file. Please refer to the already existing page configs there.

**Pro-Tip:**

If you're using PhpStorm, you can set up a [FileWatcher](https://www.jetbrains.com/help/phpstorm/2016.2/using-file-watchers.html) for the `./contents` directory and let the page generator 
automatically be executed as soon as you saved changes. You won't need to trigger the generator every time yourself. 

### 7. Commit & push your changes

**THIS IS IMPORTANT!**

**Before you commit your changes**, please generate the pages and sitemap again **without** the `--baseUrl`-option, 
so that the real base URL from the settings will take effect.

```bash
$ vendor/bin/spg.phar generate:pages ./Project.json
$ vendor/bin/spg.phar generate:sitemap ./Project.json
$ git add -A
$ git commit -m '...'
$ git push
```

### 8. Create a pull request

Please create a pull request to the origin repository. We'll then check your changes and merge them.

---

Thanks for your help!
