# Mastering WordPress Plugin & Theme Updates with GitHub

> Access the course: [Mastering WordPress Plugin & Theme Updates with GitHub](https://www.udemy.com/course/draft/6229247/?referralCode=D5603E4C41EA25771004)

**Lessons**

 1. [How the update process works](#how-the-update-process-works)
  2. [How to create the simplest WordPress theme](#how-to-create-the-simplest-wordpress-theme)
  3. [Enqueue CSS from style.css](#enqueue-css-from-stylecss)
  4. [How I recommend adding styles and scripts](#how-i-recommend-adding-styles-and-scripts)
  5. [Plugin Update Checker overview](#plugin-update-checker-overview)
  6. [GitHub integration](#github-integration)
  7. [Push your first theme update](#push-your-first-theme-update)
  8. [Push theme updates on a private repository](#push-theme-updates-on-a-private-repository)
  9. [How to create the simplest WordPress plugin](#how-to-create-the-simplest-wordpress-plugin)
  10. [Add functionality to plugin](#add-functionality-to-plugin)
  11. [Push your first plugin update](#push-your-first-plugin-update)
  12. [Conclusion](#conclusion)

## How the update process works
Tools that we'll use throughout this course:
- [Plugin Update Checker](https://github.com/YahnisElsts/plugin-update-checker)
- [Local](https://localwp.com/)
- [VS Code](https://code.visualstudio.com/download)
- [GitHub](https://github.com/)

## How to create the simplest WordPress theme

- index.php
- functions.php
- style.css

```css
/*
Theme Name: Theme Update
Description: Let's learn how to update it
Author: Your Name
Author URI: https://your-site.com
Version: 1.0
*/
```

## Enqueue CSS from style.css
```css
h1 {
  color: orange;
}
```

```php
<?php get_header(); ?>
```

```php
<?php wp_head(); ?>
```

```php
function theme_enqueue_styles() {
  wp_enqueue_style('theme-style', get_stylesheet_uri());
}
add_action('wp_enqueue_scripts', 'theme_enqueue_styles');
```

## How I recommend adding styles and scripts

```php
$theme_url = get_template_directory_uri();
$theme_version = wp_get_theme()->get('Version');
```

```php
function theme_enqueue() {
  global $theme_url;
  global $theme_version;
  wp_enqueue_style('theme-style', $theme_url . '/style.css', [], $theme_version);
  wp_enqueue_script('main-script', $theme_url . '/js/main.js', [], $theme_version);
}
add_action('wp_enqueue_scripts', 'theme_enqueue');
```

## Plugin Update Checker overview
- [Plugin Update Checker](https://github.com/YahnisElsts/plugin-update-checker)

## GitHub integration
```php
require 'plugin-update-checker/plugin-update-checker.php';
use YahnisElsts\PluginUpdateChecker\v5\PucFactory;

$myUpdateChecker = PucFactory::buildUpdateChecker(
  'https://github.com/user-name/repo-name/',
  __FILE__,
  'unique-plugin-or-theme-slug'
);

// Set the branch that contains the stable release.
$myUpdateChecker->setBranch('stable-branch-name');
```

## Push your first theme update

```git
git add .
git commit -m 'Update color'
git push
```

## Push theme updates on a private repository

```php
// Optional: If you're using a private repository, specify the access token like this:
$myUpdateChecker->setAuthentication('your-token-here');
```

## How to create the simplest WordPress plugin

- plugin-update.php
```php
<?php
/*
Plugin Name: Plugin Update
Description: Let's learn how to update it
Version: 1.0
Author: Your Name
*/
```

## Add functionality to plugin

```php
// Disable Gutenberg
add_filter('use_block_editor_for_post', '__return_false');
```

## Push your first plugin update

```php
// Update Plugin
require 'plugin-update-checker/plugin-update-checker.php';
use YahnisElsts\PluginUpdateChecker\v5\PucFactory;


$myUpdateChecker = PucFactory::buildUpdateChecker(
  'https://github.com/user-name/repo-name/',
  __FILE__,
  'unique-plugin-or-theme-slug'
);

// Set the branch that contains the stable release.
$myUpdateChecker->setBranch('stable-branch-name');

// Optional: If you're using a private repository, specify the access token like this:
$myUpdateChecker->setAuthentication('your-token-here');
```

## Conclusion
Thank you for embarking on this quick WordPress journey with me! I hope you've picked up a few new insights and feel inspired to create your own custom themes and plugins. Remember, the best way to learn is by rolling up your sleeves and getting hands-on with the code.

I'm here to support you, so please don't hesitate to reach out if you have any questions or suggestions for course updates. Your input helps me make this course even better.

If you have a moment, I would greatly appreciate it if you could leave a review on Udemy. Your feedback not only guides me but also helps fellow learners discover this course.

God bless you! Happy coding! 🧑🏻‍💻🚀
