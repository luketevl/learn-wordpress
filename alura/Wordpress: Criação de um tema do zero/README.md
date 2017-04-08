# CREATING NEW THEME

## LINKS
- https://codex.wordpress.org/Theme_Development

## STEPS
### STEP 1
- Create _folder_ in **wp-content-themes**
- Create _file_ **index.php**
- Create _file_ **style.css**

### STEP 2
- Create _file_ **header.php**
- Add function **get_head()** to get admin bar and other configurations
```html
<head>
  <?php wp_head();?>
</head>
```
- Add function **get_footer()** to configurations
```php
wp_footer();
```
- Create _file_ **functions.php**

### STEP 3
- Create _file_ **single.php** | Used for view informations of **posts**
- Create _file_ **page.php** | Used for view informations of **pages**
- Add support for **menu**
- Call menu in _header_
  - **theme_menu** | Name of _location_ defined in **functions.php**
```html
<header>
  <?php
  $args = array(
    'theme_location' => 'header-menu'
  );
    wp_nav_menu($args);
  ?>
</header>
```

### STEP 4
- _Create_ **page template**
```php

```
- _LOAD_ separated **css**

## FUNCTIONS
- Get the **header.php file**
```php
get_header();
```
- Get the **footer.php file**
```php
get_footer();
```
- Get the **admin bar** and other **resources**
```php
wp_head();
```
- Get the **resources** to **footer**
```php
wp_footer();
```
- **"The Loop"** | Loop for **posts**
  - **the_post();** | Save the post for use after
  - **the_permalink();** | Get **permalink** post
  - **the_title();** | Get **title** post
  - **the_content();** | Get **content** post
  - **the_post_thumbnail();**  | Get **featured image** post
  - **the_date();** | Get **date** post
```php
if(have_posts()){
  while(have_posts()){
    the_post();
    the_title();
    the_content();
  }
}
```
- **WP_QUERY** custom querys
```php
$args = array(
  'post_type' => type,
  'tax-query' => array(
      array(
      'taxonomy' => 'taxonomyName',
      'field'   => 'slug',
      'terms'    => 'sao-paulo'
    )
  ),
);
$loop = new WP_Query($args);
if($loop->have_posts()){
  while($loop->have_posts()){
    the_post();
    the_title();
    the_content();
  }
}
```

- _Verify_ **page**
```php
is_page('pageName');
```

- _Verify_ pages is **home**
```php
is_home();
```

- **GET taxonomies**
```php
$tax = get_terms('taxanomyName');
```
- **GET post meta**
```php
$meta = get_post_meta($post->ID);
```

- **GET BLOG informations**
  - **name** is title
```php
get_bloginfo(name);
```
- **Clean data**
```php
sanitize_text_field(param);
```
- **REDIRECT**
```php
wp_redirect();
```

### URI FUNCTIONS
- Get the **theme** **URI**
```php
get_template_directory_uri();
```
- Get the **home url**
```php
home_url();
```


### FILE FUNCTIONS.PHP
- _Added_ **support** to new exists **feature**
  - Thumbnail for post (Featured image)
```php
add_theme_support(name);
```
- _Create_ new **post type**
  - **$args** is array of _configurations_
    - **public** | Boolean, show in menu admin
    - **labels** | Array of names in post
      - **name**
      - **name_singular**
    - **supports** |  Array with **features**
```php
register_post_type('namePost', $args);
```
- **Call functions**
```php
function x(){}
do_action(when, functionName);
```
- _Added_ _support_ to **menu**
```php
register_nav_menu('locationName', 'description');
```
- _Added_ **taxonomy**
  - **args** | Options
    - **hierarchical** | Boolean, show parent taxonomy
    - **public** | Boolean, show in menu admin
    - **labels** | Array of names in taxonomy
      - **name**
      - **name_singular**
```php
register_taxonomy('name', postType, $args);
```

- _Added_ **meta box**
```php
add_meta_box('id', 'title', 'callback', 'screen', 'context', priority);
update_post_meta($post_id, key, $_REQUEST['key']); // Receive the post id in params function
add_action('save_post', functionaName);
```


# OBSERVATIONS
- To _work_ _two_ **files** are required
  - **index.php**
  - **style.css**
- _File_ **style.css**
  - have been comments about the theme
- _File_ **functions.php**
  - Added new **features** to **theme**
- **METABOX** don't work in **init** call in **add_meta_boxes**
```php
add_action('add_meta_boxes', functionName);
```
