
# Tutorial WooCommerce

## Set up an open source e-store for WordPress

With external plugin support, your WordPress blog can evolve into an ecommerce platform

![](img/a54b3b473771472dd2321ddda1014be1_35_0.png)

One of the biggest revolutions that the Internet has brought to our connected society is the ability to shop online. You can stay in the comfort of your own home and you might need nothing but a working connection and a device to connect to. With commerce you can sell products and services from your own shop. This has made business much more viable than it has been. Given this rise anyone can set up their own with minimal technology.

## 01 Install WordPress

Several hosting providers have these days that are more of a one-click install WordPress. However, if you are more of a person or want to do it on your local machine first before taking it, it is important to first learn to install and configure WordPress and then create a user and assign privileges to the user so that they can access the WordPress database. To do this, follow the steps in a terminal window:

```
$ mysql -u root -p
CREATE DATABASE WordPress;
GRANT ALL PRIVILEGES ON WordPress.* TO 'wordpress'@'localhost' IDENTIFIED BY 'password';
FLUSH PRIVILEGES;
```

Note that after the first step, you will need to enter the password for MySQL. By default there is no password assigned, so if you are not remembering it, you can

While there are several proprietary solutions available for this, open source is not far behind. We will take a look at them all. WooCommerce is an open source plugin that integrates seamlessly with WordPress. Once you set it up, it extends everything in this tutorial we will run through the steps to install and use WordPress and WooCommerce to create your own web shop and start selling items. We will also take a look at the administrative aspects of a WooCommerce web shop and how to use it effectively.

| Products | Name | SKU | Price | Status | Visibility | Tax | Stock | Actions |
|---|---|---|---|---|---|---|---|---|
| T-shirt | T-shirt | ts-01 | $20.00 | Published | Visible | | 15 in stock | edit delete trash view edit |
| Hoodie | Hoodie | hd-01 | $40.00 | Published | Visible | | 10 in stock | edit delete trash view edit |
| Cap | Cap | cp-01 | $15.00 | Published | Visible | | 25 in stock | edit delete trash view edit |
| Socks | Socks | sk-01 | $5.00 | Published | Visible | | 100 in stock | edit delete trash view edit |
| Belt | Belt | be-01 | $25.00 | Published | Visible | | 20 in stock | edit delete trash view edit |

## Start with WooCommerce

![](img/a54b3b473771472dd2321ddda1014be1_36_0.png)

Just Enter the prompt and you'll be ready. Next step is to download WordPress and set up the configuration file. You can download the stable configuration from their server, upload and place the contents in the root of your folder. Then use sample file (wp-config-sample.php) to create the actual file (rename it wp-config.php). Once this is done, open the config file and update with values.

> With ecommerce becoming main, the cost of starting with your shop has gone down several notches.

- Adding new products is very much new web posts.

## 02 Install WooCommerce

Now that the config is set, start the web server and open the default page. You should see the WordPress registration page. Enter your username, password and email id. Then you have WordPress installation ready. The next step is to install WooCommerce by downloading the WooCommerce plugin from their website, extract the files to the webroot folder. Log in to WordPress and go to the Plugins page on the left menu bar, click Add New and Search for WooCommerce then install the plugin. Activate directly from there. If you encounter errors related to permissions, to solve them, you will need to create folders and change them now.

Browse for the folder dummy-data (inside the WooCommerce source) and then select the dummy-data.xml in the text, select the user you want to attribute to all content and check the box that says "Import only". Now you have all content on your site. To cross-check, click on Products link on the menu bar and see your products listed.

## 03 Import data

Now that you want to test the various features and that you have the necessary content ready to populate your shop, it is time to import the dummy data to WooCommerce installation. This will make it clearer as you explore WooCommerce. A dummy data is available on the WooCommerce source folder itself. To import it use ImportWP. If not already installed, will install the WordPress import plugin. Once installed, click on Activate and import now.

Since we already imported data, you will see many products listed. To add a new product is easy; just click on Add Product link. In the product page that appears, fill in the product details like name, description, price and image. With the WooCommerce blog post feature, find this very page, with one important change. By the description field, you will find the product data, and this is where all the specific settings are. These settings include product, general settings, inventory related settings, shipping, linked products and product attributes.

```
$ sudo wp-cli --user=www-data
```

## Using Pusher

The Pusher plugin integrates your shop with the Pusher service for Android and iOS. You can install it to get automatic notifications for real-time new orders, out of stock notifications:
Get it here: github.com/npusher-woocommerce

## 04 Start with WooCommerce

Now that you have installed WooCommerce, you will get new menus on the left menu bar. WooCommerce you'll find all the business items, like coupons, coupons management, system status and so under WooCommerce. Products section which related to products like their categories, tags, etc. Let's start the Products section.

# Tutorial WooCommerce

![](img/a54b3b473771472dd2321ddda1014be1_37_0.png)

Right, you'll need to work with Simple products, Grouped products comprise these:

- Choosing the right look
Users are split for choice, especially on economics. So, it's important that your WooCommerce website has a nice look and feel. If you want, check out our: github.com/jeamsmith/woocommerce-guide.

## 05 Product types and settings

By default there are four product types. The first product type is Simple: used for standalone products. Next is Grouped: a collection of related products that can be purchased individually. An External or Affiliate product is something that is sold outside of your site. A Variable product has variations that have different SKU, price and stock quantity. For the virtual and downloadable product, it is used to sell digital items.

## 06 More settings

The General tab allows you to set the regular price and sale price for a product. You can also choose to schedule the sale for a limited time. In the Inventory tab, you can manage stock at the product level – this way, the number of items in stock will be tracked and updated after every sale. Linked Products can be used to set related products for upsells and cross-sells. This displays recommends products on products with attributes like size, color, and etc., to the product page. There is Advanced tab to help you set an optional product note to be sent to customers after a purchase, and to enable reviews, set customer menus under etc. The product settings fields, you can also find the short description on the product page. If you fill it in, that short description will be available on the product page.

## 07 WooCommerce settings

Now that you have an idea of how to manage products in WooCommerce, let's take a look at basic settings. In WooCommerce settings to see the settings pages with different tabs. To start, check out Checkout. You can find basic settings here location, shipping, and tax. The Products tab manages units, product downloads, downloadable settings. Under the tax tab, you can enable tax-related calculations for products and services. The Checkout tab allows you to set like coupons code, supported payment methods. The Shipping tab is for setting up shipping zones and methods. The Accounts tab helps set up the users accounts management, password management and the login. The Emails tab lets you set out the notifications for various matters during the order life. The API tab is used for integrating WooCommerce with other plugins. You can use- REST APIs for the integration.
