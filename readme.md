[![Latest Stable Version](https://poser.pugx.org/fish/laravel-tabs/v/stable.svg)](https://packagist.org/packages/fish/laravel-tabs) [![Total Downloads](https://poser.pugx.org/fish/laravel-tabs/downloads.svg)](https://packagist.org/packages/fish/laravel-tabs) [![Latest Unstable Version](https://poser.pugx.org/fish/laravel-tabs/v/unstable.svg)](https://packagist.org/packages/fish/laravel-tabs) [![License](https://poser.pugx.org/fish/laravel-tabs/license.svg)](https://packagist.org/packages/fish/laravel-tabs)

# Easily create Bootstrap tabs in your Laravel app

This Laravel 4 package provides an artisan command to easily generate bootstrap tabs.
The package creates a unique view for each tab, and allows you to embed the tabs wherever you need in your HTML.
This makes for a clean uncluttered code, and allows you to skip the tedious process of writing the HTML yourself and focus on the content of the tabs.

- [Installation](#installation)
- [Usage](#usage)
    - [Generate the tabs](#generate-the-tabs)
    - [Fill the views with content](#fill-the-views-with-content)
    - [Pull the tabs into your view](#pull-the-tabs-into-your-view)
- [Config](#config)

## Installation

Begin by installing this package through Composer. Edit your project's `composer.json` file to require `fish/easy-tabs`.

	"require": {
		"fish/laravel-tabs": "dev-master"
	}

Next, update Composer from the Terminal:

    composer update

Once this operation completes, the final step is to add the service provider. Open `app/config/app.php`, and add a new item to the providers array.

    'Fish\Tabs\TabsServiceProvider'

On the client-side remember to include bootstrap's CSS and JavaScript files. The quickest way is using a CDN:

    <link href="//maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap.min.css" rel="stylesheet">
    <script src="//maxcdn.bootstrapcdn.com/bootstrap/3.2.0/js/bootstrap.min.js"></script>

That's it! You're all set to go. Run the `artisan` command from the Terminal to see the new `tabs` command.

    php artisan

## Usage

### Generate the tabs

Start by creating the tabs from the command line.
The basic syntax is:

    php artisan tabs:generate [key] [--tabs="list-of-tabs"]

First provide the key, which you will use later to grab the tabs, and then list the tabs.
The tabs should be entered as a comma separated list. The words are spearated by default with an underscore.
Of course, when presented in the view they will be separated by spaces. As for capitaliztion, by default the first word will be uppercase.

if you want to create a tab with dropdown menu the syntax is `main_tab:sub_tab1|sub_tab2`.

Example:

    php artisan tabs:generate article --tabs="section1, section2, section3:sub_section1|sub_section2"

Note that the key is also used by default to set the name of the folder, where the tabs partials will be created.

### Fill the views with content

The views will reside by default under `app/views/[key]`.

### Pull the tabs into your view

In your controller you simply pass a variable to the view:

    return View::make('some.view', ['tabs'=>Tabs::get('article')]);

Then in your view echo `$tabs` wherever you want the tabs to appear.

## Config

The package allows you to config a few options, namely:

1. Tabs type: tabs or pills.
2. Tabs direction: horizontal or vertical.
3. The path where the tabs views will be created relative to the views folder. Defaults to the key used when creating the tabs.
4. The separator between words to be used in the artisan command. Default: _
5. Whether or not to use a fade effect. Default: true
6. Capitalization of the titles. Options: first_word, all_words, no_words. Default: first_word
7. Path to the json file which saves the tabs data.

To change the configuration you need to publish it to your project first:

     php artisan config:publish fish/laravel-tabs

The path to the published file is:

    app/config/packages/fish/laravel-tabs/config.php