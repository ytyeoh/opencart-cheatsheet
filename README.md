# delete order
	DELETE FROM `ocun_order` WHERE `order_id` BETWEEN 110 AND 118;
	DELETE FROM `ocun_order_history` WHERE `order_id` BETWEEN 110 AND 118;
	DELETE FROM `ocun_order_product` WHERE `order_id` BETWEEN 110 AND 118;
	DELETE FROM `ocun_order_total` WHERE `order_id` BETWEEN 110 AND 118;
	DELETE FROM `ocun_order_voucher` WHERE `order_id` BETWEEN 110 AND 118;
	DELETE FROM `ocun_order_shipment` WHERE `order_id` BETWEEN 110 AND 118;
	
# downoad all products 
	SELECT p.product_id AS id, p.model, pd.name, p.price, pf.filter_id, GROUP_CONCAT(pc.category_id SEPARATOR ';') AS CategoryId, IFNULL((SELECT COUNT(*) 
	    FROM ocun_product_image 
	   WHERE ocun_product_image.product_id = p.product_id
	   GROUP BY ocun_product_image.product_id),0) -1 AS Extra_Images
	FROM ocun_product p
	LEFT JOIN ocun_product_description pd USING (product_id)
	LEFT JOIN ocun_product_filter pf USING (product_id)  
	LEFT JOIN ocun_product_to_category pc USING (product_id)
	WHERE pd.language_id = 2
	GROUP BY pc.product_id
	ORDER BY `id` ASC
# window curl fix

			curl_setopt($ch, CURLOPT_SSL_VERIFYHOST, false);
			curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, false);

# rename filename ext

	find . -iname "*.JPG" -exec bash -c 'mv "$0" "${0%\.JPG}.jpg"' {} \;
	find . -iname "*.png" -exec bash -c 'mv "$0" "${0%\.png}.jpg"' {} \;
	find . -iname "*.jpeg" -exec bash -c 'mv "$0" "${0%\.jpeg}.jpg"' {} \;
	find . -iname "*.JPEG" -exec bash -c 'mv "$0" "${0%\.JPEG}.jpg"' {} \;


# opencart-cheatsheet
Reset Opencart product 
      ALTER TABLE ocmv_category  AUTO_INCREMENT = 1;
      DELETE FROM ocmv_category WHERE category_id > 0;

# opencart-cheatsheet delete category
	DELETE FROM ocmv_category_description WHERE category_id > 0;
	ALTER TABLE ocmv_category_description AUTO_INCREMENT = 1;
	DELETE FROM ocmv_category_path WHERE category_id > 0;
	ALTER TABLE ocmv_category_path AUTO_INCREMENT = 1;
	DELETE FROM ocmv_category_to_store WHERE category_id > 0;
	ALTER TABLE ocmv_category_to_store AUTO_INCREMENT = 1;
	DELETE FROM ocmv_category_to_layout WHERE category_id > 0;
	ALTER TABLE ocmv_category_to_layout AUTO_INCREMENT = 1;

# opencart-cheatsheet delete product
	ALTER TABLE ocmv_product AUTO_INCREMENT = 1;
	DELETE FROM ocmv_product WHERE product_id > 0;
	DELETE FROM ocmv_product_attribute WHERE product_id > 0;
	DELETE FROM ocmv_product_description WHERE product_id > 0;
	ALTER TABLE ocmv_product_discount AUTO_INCREMENT = 1;
	DELETE FROM ocmv_product_discount WHERE ocmv_producty_discount_id > 0;
	ALTER TABLE ocmv_product_image  AUTO_INCREMENT = 1;
	DELETE FROM ocmv_product_image WHERE product_image_id > 0;
	ALTER TABLE ocmv_product_option  AUTO_INCREMENT = 1;
	DELETE FROM ocmv_product_option WHERE product_option_id > 0;
	ALTER TABLE ocmv_product_option_value  AUTO_INCREMENT = 1;
	DELETE FROM ocmv_product_option_value WHERE product_option_value_id > 0;
	ALTER TABLE ocmv_product_related  AUTO_INCREMENT = 1;
	DELETE FROM ocmv_product_related WHERE product_option_value_id > 0;
	ALTER TABLE ocmv_product_reward  AUTO_INCREMENT = 1;
	DELETE FROM ocmv_product_reward WHERE product_reward_id > 0;
	ALTER TABLE ocmv_product_special AUTO_INCREMENT = 1;
	DELETE FROM ocmv_product_special WHERE product_special_id > 0;
	DELETE FROM ocmv_product_categoty WHERE product_id > 0;
	DELETE FROM ocmv_product_to_store WHERE product_id > 0;




#category
DELETE FROM `ocun_demo1category` WHERE category_id > 0;
DELETE FROM `ocun_demo1category_description` WHERE category_id > 0;
DELETE FROM `ocun_demo1category_to_layout` WHERE category_id > 0;
DELETE FROM `ocun_demo1category_to_store` WHERE category_id > 0;
DELETE FROM `ocun_demo1category_path` WHERE category_id > 0;
