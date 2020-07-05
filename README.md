# window curl fix

			curl_setopt($ch, CURLOPT_SSL_VERIFYHOST, false);
			curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, false);



# opencart-cheatsheet
Reset Opencart product 
      ALTER TABLE ocmv_category  AUTO_INCREMENT = 1;
      DELETE FROM ocmv_category WHERE category_id > 0;


DELETE FROM ocmv_category_description WHERE category_id > 0;
DELETE FROM ocmv_category_path WHERE category_id > 0;
DELETE FROM ocmv_category_to_store WHERE category_id > 0;
DELETE FROM ocmv_category_to_layout WHERE category_id > 0;


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
