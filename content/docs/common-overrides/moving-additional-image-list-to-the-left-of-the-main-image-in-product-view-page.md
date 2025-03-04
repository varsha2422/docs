---
path: "/docs/Common-overrides/moving-additional-image-list-to-the-left-of-the-main-image-in-product-view-page"
updated: "2019-06-12"
title: "Moving additional image list to the left of the main image in product view page"
description: ""
author: "Sowbagya lakshmi"
category: "Common-overrides"
---

If you are trying to move the additional images to the left side of the main image in the product item view page, then it is possible by creating an override as follows:

**Steps to be done: **

* Create a file called "view_images.php" under "/templates/your site's template/html/com_j2store/templates/your sub-template/" 
* Paste the following code there:

  <link-text url="https://gist.github.com/sowbagyalakshmi/1af8edb51d8b8becd40da89547e7e9f2" target="_blank" rel= "noopener">	Click to open the gist code</link-text>

  
```
<?php

/**
 * @package J2Store
 * @copyright Copyright (c)2014-17 Ramesh Elamathi / J2Store.org
 * @license GNU GPL v3 or later
 */

// No direct access
defined('_JEXEC') or die;
$image_path = JUri::root();
$main_image = "";
$main_image_width = $this->params->get('item_product_main_image_width', '200');
$additional_image_width = $this->params->get('item_product_additional_image_width', '100');
?>
<?php if ($this->params->get('item_show_product_additional_image', 1) && isset($this->product->additional_images) && !empty($this->product->additional_images)) : ?>
    <?php
    $additional_images = json_decode($this->product->additional_images);
    $additional_images = array_filter((array) $additional_images);
    if (count($additional_images)) :
        ?>
        <?php if ($this->params->get('item_show_product_main_image', 1) && !empty($this->product->main_image)) : ?>
            <div class="j2store-mainimage span7 pull-right">
                <?php $main_image = $this->product->main_image; ?>
                <?php if ($main_image &&  JFile::exists(JPATH_SITE . '/' . $main_image)) : ?>
                    <?php $class = $this->params->get('item_enable_image_zoom', 1) ? 'zoom' : 'nozoom'; ?>

                    <span class="<?php echo $class; ?>" id="j2store-item-main-image-<?php echo $this->product->j2store_product_id; ?>">
                        <img itemprop="image" alt="<?php echo $this->product->product_name; ?>" title="<?php echo $this->product->product_name; ?>" class="j2store-product-main-image j2store-img-responsive" src="<?php echo $image_path . $main_image; ?>" width="<?php echo intval($main_image_width); ?>" />`
                    </span>
                    <script type="text/javascript">
                        var main_image = "<?php echo $image_path . $main_image; ?>";
                        j2store.jQuery(document).ready(function() {
                            var enable_zoom = < ? php echo $this - > params - > get('item_enable_image_zoom', 1); ? > ;
                            if (enable_zoom) {
                                j2store.jQuery('#j2store-item-main-image-<?php echo $this->product->j2store_product_id; ?>').zoom();
                            }
                        });
                    </script>
                <?php elseif (!empty($this->product->main_image)) : ?>
                    <?php echo J2Store::product()->displayImage($this->product, array('type' => 'ViewMain', 'params' => $this->params)); ?>
                <?php endif; ?>
            </div>

        <?php endif; ?>
        <div class="j2store-product-additional-images span5">

            <ul class="additional-image-list">
                <?php
                foreach ($additional_images as $key => $image) : ?>
                    <?php
                    if (JFile::exists(JPATH_SITE . '/' . $image)) :
                        $image_src = $image_path . $image;
                        ?>
                        <li>
                            <img onmouseover="setMainPreview('addimage-<?php echo $this->product->j2store_product_id; ?>-<?php echo $key; ?>', <?php echo $this->product->j2store_product_id; ?>, <?php echo $this->params->get('item_enable_image_zoom', 1); ?>, 'inner')" onclick="setMainPreview('addimage-<?php echo $this->product->j2store_product_id; ?>-<?php echo $key; ?>', <?php echo $this->product->j2store_product_id; ?>, <?php echo $this->params->get('item_enable_image_zoom', 1); ?>, 'inner')" id="addimage-<?php echo $this->product->j2store_product_id; ?>-<?php echo $key; ?>" class="j2store-item-additionalimage-preview j2store-img-responsive" src="<?php echo $image_src; ?>" alt="<?php echo $this->product->product_name; ?>" title="<?php echo $this->product->product_name; ?>" width="<?php echo intval($additional_image_width); ?>" />
                        </li>
                    <?php elseif (!empty($image)) : ?>
                        <?php echo J2Store::product()->displayImage($this->product, array('type' => 'ViewAdditional', 'params' => $this->params, 'key' => $key, 'image' => $image)); ?>

                    <?php endif; ?>
                <?php endforeach; ?>
            <?php endif; ?>
        <?php endif; ?>
        <?php if ($main_image &&  JFile::exists(JPATH_SITE . '/' . $main_image)) : ?>
            <li>`
                <img onmouseover="setMainPreview('additial-main-image-<?php echo $this->product->j2store_product_id; ?>', <?php echo $this->product->j2store_product_id; ?>, <?php echo $this->params->get('item_enable_image_zoom', 1); ?>, 'inner')" onclick="setMainPreview('additial-main-image-<?php echo $this->product->j2store_product_id; ?>', <?php echo $this->product->j2store_product_id; ?>, <?php echo $this->params->get('item_enable_image_zoom', 1); ?>, 'inner')" id="additial-main-image-<?php echo $this->product->j2store_product_id; ?>" alt="<?php echo $this->product->product_name; ?>" title="<?php echo $this->product->product_name; ?>" class="j2store-item-additionalimage-preview j2store-img-responsive additional-mainimage" src="<?php echo $image_path . $main_image; ?>" width="<?php echo intval($additional_image_width); ?>" />
            </li>
        <?php elseif (!empty($this->product->main_image)) : ?>
            <?php echo J2Store::product()->displayImage($this->product, array('type' => 'AdditionalMain', 'params' => $this->params)); ?>
        <?php endif; ?>
    </ul>
</div>

<?php if ($this->params->get('item_enable_image_zoom', 1)) : ?>
    <script>
        j2store.jQuery(document).ready(function() {
            j2store.jQuery('body').on('after_doAjaxFilter', function(e, product, response) {
                j2store.jQuery('img.zoomImg').remove();
                j2store.jQuery('#j2store-item-main-image-<?php echo $this->product->j2store_product_id; ?>').zoom();
            });
        });
    </script>
<?php endif; ?>


```


Save.
This would display the additional images list to the left of the main image on the product's item view
