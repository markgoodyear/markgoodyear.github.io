---
title: "Quick tip: Display page ID&#39;s in the WordPress admin area"
slug: "display-page-id-wordpress-admin-area"
layout: post
published: true
date: 2013-07-09
---

<p class="lead">In a WordPress site with many pages, it can become tedious to try find the ID of a page. With this simple script, the page ID is displayed right next to each page. No plugins needed!</p>

To display the page ID next to the page title, simply add this snippet to your themes `functions.php` file:

{% highlight php %}
<?php

// Set columns to be used in the Pages section
function custom_set_pages_columns($columns) {
    return array(
        'cb'      => '<input type="checkbox" />',
        'page_id' => __('ID'),
        'title'   => __('Title'),
        'author'  => __('Author'),
        'date'    => __('Date')
    );
}

// Add the ID to the page ID column
function custom_set_pages_columns_page_id($column, $post_id) {
    if ($column == 'page_id') {
        echo $post_id;
    }
}

// Add custom styles to the page ID column
function custom_admin_styling() {
    echo '<style type="text/css">',
         'th#page_id { width:60px; }',
         '</style>';
}

// Add filters and actions
add_filter('manage_edit-page_columns',   'custom_set_pages_columns');
add_action('manage_pages_custom_column', 'custom_set_pages_columns_page_id', 10, 2);
add_action('admin_head',                 'custom_admin_styling');

?>
{% endhighlight %}

Your Pages admin section should now look something like this:

<p class="post-img  text--center">
    <img src="http://markgoodyear.com/images/posts/wordpress-page-id.png" alt="WordPress Page ID">
</p>

Now you can easily check the ID of any page. If anyone has any other (or better) methods, please let me know via the comments below or send me a <a href="http://twitter.com/markgdyr">Tweet</a>.
