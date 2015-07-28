=== WooCommerce Last Purchased ===
Contributors: (DawidUrbanski)
Tags: woocommerce
Requires at least: 4.2
Tested up to: 4.2.2
Stable tag: 1.0
License: GPLv2 or later
License URI: http://www.gnu.org/licenses/gpl-2.0.html

This is WooCommerce plugin. It shows last purchased date on each product page.

== Description ==

This little WooCommerce plugin shows last purchased date on single product page. It shows last purchase date made by anyone, not just current user. If current product has no sales yet, popup will not appear.

= Why would I show this to my customers? =

From my experience, showing last purchased date can increase conversion rate. This trick is using by Allegro ([www.allegro.pl](http://allegro.pl)), biggest auction and sales website in Poland.

== Installation ==

= From WordPress dashboard =

1. Log in to you WordPress dashboard.
2. Navigate to plugins page and to "Add new" next.
3. Type "WooCommerce Last Purchased" in search field.
4. Install and activate plugin.

= Manually place plugin files in your plugins directory =

1. Download and unzip plugin files.
2. Copy plugin folder (`woocommerce-last-purchased`) to your Wordpress installation plugins directory (`/wp-content/plugins/`).
3. Go to you WordPress panel, to plugins page.
4. Activate plugin.

Install plugin from your WordPress dashboard

== Usage ==

= Basic usage =

Just install plugin and you are ready to go.

= Using just date in your theme (and hide popup if needed) =

So you want to get last purchased date somewhere in your theme files? No problem.

**First way: using WooCommerce hooks**

In you function.php file paste below code.

`function show_last_purchased_date(){

	if ( WLP()->last_purchased_date() ){
		echo '<div class="last-purchased-date">' . WLP()->last_purchased_text()
		        . ': ' . WLP()->last_purchased_date() . '</div>';
	}

}
add_action('woocommerce_product_meta_end', 'show_last_purchased_date');`

For more information about WooCommerce hooks, please visit [WooCommerce documentation](http://docs.woothemes.com/document/introduction-to-hooks-actions-and-filters/).

**Second way: override WooCommerce template**

You can achieve exact same result by overriding WooCommerce templates.

You will need to override one of WooCommerce templates. In this case we will put this information right after Add to cart button and SKU.

For more information about this, please visit [WooCommerce documentation](http://docs.woothemes.com/document/template-structure/).

1. Go to your woocommerce plugin directory.
2. Go to `templates` directory.
3. Go to `single-product`.
4. Copy `meta.php` file to 'your_theme_directory/woocommerce/single-product/'.
5. If you don't have such directory, create it.
6. Now add below code just before `<?php do_action( 'woocommerce_product_meta_end' ); ?>`


`<?php if ( WLP()->last_purchased_date() ): ?>

    <div class="last-purchased-date">
        <?php echo WLP()->last_purchased_text(); ?>:
        <?php echo WLP()->last_purchased_date(); ?>
    </div>

<?php endif; ?>`

**Don't show popup**

In your functions.php:

`function hide_wlp_popup(){

	WLP()->hide_popup = true;

}
add_action('before_wlp_init', 'hide_wlp_popup');`

= Styling =

You can override popup styles. Just place your rules in your theme `style.css` file. Couple examples below.

= Display popup in bottom left corner instead of bottom right =

`.wlp-popup{

    left: 15px;
    right: auto;
    margin-right: 15px;

}`

= Change background and text color =

`.wlp-popup{

	background: rgba(98,233,219,0.9);
    color:#0b413b;

}`

= Remove rounded corners, non-transparent background, no X button =

`.wlp-popup{

	background: #76234c;
	border-radius: 0;

}

.wlp-popup-close{

    display:none;

}`

== Translations ==

This plugin is translation ready. You can help by translating this plugin into your language. All languages are stored in `languages` directory.

= `Time ago` text translation. =

This plugin uses [timeago.js](https://github.com/rmm5t/jquery-timeago) jQuery plugin. This plugin is also ready for translations. You can find all available languages [here](https://github.com/rmm5t/jquery-timeago/tree/master/locales). If your language is not available in `timeago.js` plugin, you will need to create such translation as well.

== TODO List ==

This plugin is free, and I have got limited time. However I will try to implement following features in near future:

* Add options to WordPress admin area:
    * show/hide close button,
    * popup appear settings,
    * custom css field,
* Ability to override popup html to your own.


== License ==

This plugin is released under GPLv2 license. This plugins is free to use both in personal and commercial usage. It's distributed "as is", and no support from the author is provided.

== Special thanks ==

Special thanks to [Ryan McGeary](https://github.com/rmm5t) ([http://ryan.mcgeary.org](http://ryan.mcgeary.org)), author of [timeago.js](https://github.com/rmm5t/jquery-timeago), jQuery plugin used in this little project.