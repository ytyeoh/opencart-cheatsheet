# opencart csv
	SELECT op.product_id AS id, opd.name AS title, opd.description AS rich_text_description, 'In Stock' AS availability, 'new' AS 'condition', op.price, concat('https://changshenfood.com/index.php?route=product/product&product_id=', op.product_id) AS link, concat('https://changshenfood.com/image/', op.image) AS image_link, op.mpn AS brand, concat('https://changshenfood.com/image/', opi.image) AS additional_image_link, concat('category__', opc.category_id) AS google_product_category from  ocun_product op LEFT JOIN ocun_product_description opd ON opd.product_id = op.product_id LEFT JOIN ocun_product_image opi ON opi.product_id = op.product_id  LEFT JOIN ocun_product_to_store ops ON ops.product_id = op.product_id LEFT JOIN ocun_product_to_category opc ON opc.category_id = (SELECT opc1.category_id FROM ocun_product_to_category opc1 WHERE opc1.product_id = op.product_id ORDER BY opc1.category_id DESC LIMIT 1) WHERE opd.language_id= 1 AND ops.store_id = 1;
	
IFS(K2="category__211","Food, Beverages & Tobacco > Beverages > Hot Chocolate",k2="category__212","Food, Beverages & Tobacco > Beverages > Coffee",k2="category__214","Food, Beverages & Tobacco > Beverages > Non-Dairy Milk",k2="category__215","Food, Beverages & Tobacco > Beverages > Milk",K2="category__217","Food, Beverages & Tobacco > Beverages > Tea & Infusions",k2="category__218","Food, Beverages & Tobacco > Beverages > Alcoholic Beverages",k2="category__219","Food, Beverages & Tobacco > Beverages > Water",k2="category__220","Food, Beverages & Tobacco > Beverages > Powdered Beverage Mixes",K2="category__216","Food, Beverages & Tobacco > Beverages > Soda",k2="category__221","Food, Beverages & Tobacco > Beverages > Juice",k2="category__311","Food, Beverages & Tobacco > Food Items > Cooking & Baking Ingredients",k2="category__312","Food, Beverages & Tobacco > Food Items > Cooking & Baking Ingredients",k2="category__313","Food, Beverages & Tobacco > Food Items > Condiments & Sauces",k2="category__314","Food, Beverages & Tobacco > Food Items",k2="category__315","Food, Beverages & Tobacco > Food Items > Soups & Broths",K2="category__316","Food, Beverages & Tobacco > Food Items > Snack Foods",k2="category__317","Food, Beverages & Tobacco > Food Items > Prepared Foods",k2="category__511","Home & Garden > Household Supplies > Household Paper Products",k2="category__512","Home & Garden > Household Supplies > Laundry Supplies > Laundry Detergent",K2="category__513","Health & Beauty > Personal Care > Hair Care",k2="category__515","Health & Beauty > Personal Care",k2="category__3111","Food, Beverages & Tobacco > Food Items > Cooking & Baking Ingredients > Flour",k2="category__3112","Food, Beverages & Tobacco > Food Items > Cooking & Baking Ingredients",k2="category__3113","Food, Beverages & Tobacco > Food Items > Cooking & Baking Ingredients",k2="category__3114","Food, Beverages & Tobacco > Food Items > Dips & Spreads > Jams & Jellies",k2="category__3121","Food, Beverages & Tobacco > Food Items > Fruits & Vegetables > Canned & Prepared Beans",K2="category__3121","Food, Beverages & Tobacco > Food Items > Condiments & Sauces",k2="category__3123","Food, Beverages & Tobacco > Food Items > Cooking & Baking Ingredients > Cooking Oils",k2="category__3124","Food, Beverages & Tobacco > Food Items > Seasonings & Spices",k2="category__3125","Food, Beverages & Tobacco > Food Items > Seasonings & Spices > Herbs & Spices",K2="category__3126","Food, Beverages & Tobacco > Food Items > Cooking & Baking Ingredients",k2="category__3127","Food, Beverages & Tobacco > Food Items > Cooking & Baking Ingredients",k2="category__3132","Food, Beverages & Tobacco > Food Items > Seasonings & Spices > Herbs & Spices",k2="category__3131","Food, Beverages & Tobacco > Food Items > Seasonings & Spices > Herbs & Spices",k2="category__3141","Food, Beverages & Tobacco > Food Items > Pasta & Noodles",k2="category__3142","Food, Beverages & Tobacco > Food Items > Pasta & Noodles",k2="category__3143","Food, Beverages & Tobacco > Food Items > Grains, Rice & Cereal > Rice",K2="category__3151","Food, Beverages & Tobacco > Food Items > Soups & Broths",k2="category__3161","Food, Beverages & Tobacco > Food Items > Bakery > Cookies",k2="category__3162","Food, Beverages & Tobacco > Food Items > Snack Foods > Chips",k2="category__3163","Food, Beverages & Tobacco > Food Items > Bakery > Breads & Buns",k2="category__3122","Food, Beverages & Tobacco > Food Items > Condiments & Sauces")



# delete order
	DELETE FROM `ocun_order` WHERE `order_id` BETWEEN 110 AND 118;
	DELETE FROM `ocun_order_history` WHERE `order_id` BETWEEN 110 AND 118;
	DELETE FROM `ocun_order_product` WHERE `order_id` BETWEEN 110 AND 118;
	DELETE FROM `ocun_order_total` WHERE `order_id` BETWEEN 110 AND 118;
	DELETE FROM `ocun_order_voucher` WHERE `order_id` BETWEEN 110 AND 118;
	DELETE FROM `ocun_order_shipment` WHERE `order_id` BETWEEN 110 AND 118;


# downalod products without category
	  SELECT p.product_id AS id, p.model, p.sku, pd.name as name_eng, pd1.name as name_mix, pd2.name as name_cn,   p.price
  	FROM ocun_product p
  	LEFT JOIN ocun_product_description pd USING (product_id)
  	LEFT JOIN ocun_product_description pd1 USING (product_id)
	  LEFT JOIN ocun_product_description pd2 USING (product_id)

	  WHERE p.product_id > 0 
	  AND pd.language_id = 2
	  and pd1.language_id = 1
	  and pd2.language_id = 6
	  GROUP BY p.product_id
	  ORDER BY `id` ASC
# downoad all products 
	SELECT p.product_id, p.model, p.sku, pd.name as chinese_name, pd2.name as english_name, p.price, p.manufacturer_id AS manufacture_id, GROUP_CONCAT(pc.category_id SEPARATOR ';') AS category_id,  GROUP_CONCAT(pf.filter_id SEPARATOR ';') AS filter, IFNULL((SELECT COUNT(*) 
  	FROM ocun_product_image 
  	 WHERE ocun_product_image.product_id = p.product_id
  	 GROUP BY ocun_product_image.product_id),0) -1 AS total_image, 
	   pd.description as description_chinese, pd2.description as description_english, IF(p.product_id IS NULL, 'no selected', '1') AS company_id
	  FROM ocun_product p
	  LEFT JOIN ocun_product_description pd USING (product_id)
	  LEFT JOIN ocun_product_description pd1 USING (product_id)
	  LEFT JOIN ocun_product_description pd2 USING (product_id)
	  LEFT JOIN ocun_product_filter pf USING (product_id)  
	  LEFT JOIN ocun_product_to_category pc USING (product_id)
	  WHERE pd.language_id = 2
	  and pd1.language_id = 1
	  and pd2.language_id = 6
	  GROUP BY pc.product_id
	  ORDER BY p.product_id ASC
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
	DELETE FROM ocun_category WHERE category_id > 0;
	ALTER TABLE ocun_category AUTO_INCREMENT = 1;
	DELETE FROM ocun_category_description WHERE category_id > 0;
	ALTER TABLE ocun_category_description AUTO_INCREMENT = 1;
	DELETE FROM ocun_category_path WHERE category_id > 0;
	ALTER TABLE ocun_category_path AUTO_INCREMENT = 1;
	DELETE FROM ocun_category_to_store WHERE category_id > 0;
	ALTER TABLE ocun_category_to_store AUTO_INCREMENT = 1;
	DELETE FROM ocun_category_to_layout WHERE category_id > 0;
	ALTER TABLE ocun_category_to_layout AUTO_INCREMENT = 1;

# opencart-cheatsheet delete product
	ALTER TABLE `ocun_product` CHANGE `date_available` `date_available` DATE NOT NULL;
	ALTER TABLE ocun_product AUTO_INCREMENT = 1;
	DELETE FROM ocun_product WHERE product_id > 0;
	DELETE FROM ocun_product_attribute WHERE product_id > 0;
	DELETE FROM ocun_product_description WHERE product_id > 0;
	DELETE FROM ocun_product_discount WHERE product_discount_id > 0;
	ALTER TABLE `ocun_product_discount` CHANGE `date_start` `date_start` DATE NOT NULL, CHANGE `date_end` `date_end` DATE NOT NULL;
	ALTER TABLE ocun_product_discount AUTO_INCREMENT = 1;
	ALTER TABLE ocun_product_image  AUTO_INCREMENT = 1;
	DELETE FROM ocun_product_image WHERE product_image_id > 0;
	ALTER TABLE ocun_product_option  AUTO_INCREMENT = 1;
	DELETE FROM ocun_product_option WHERE product_option_id > 0;
	ALTER TABLE ocun_product_option_value  AUTO_INCREMENT = 1;
	DELETE FROM ocun_product_option_value WHERE product_option_value_id > 0;
	ALTER TABLE ocun_product_related  AUTO_INCREMENT = 1;
	DELETE FROM ocun_product_related WHERE product_id > 0;
	ALTER TABLE ocun_product_reward  AUTO_INCREMENT = 1;
	DELETE FROM ocun_product_reward WHERE product_reward_id > 0;
	DELETE FROM ocun_product_special WHERE product_special_id > 0;
	ALTER TABLE `ocun_product_special` CHANGE `date_start` `date_start` DATE NOT NULL, CHANGE `date_end` `date_end` DATE NOT NULL;
	ALTER TABLE ocun_product_special AUTO_INCREMENT = 1;
	DELETE FROM ocun_product_to_category WHERE product_id > 0;
	DELETE FROM ocun_product_to_store WHERE product_id > 0;
	ALTER TABLE ocun_attribute AUTO_INCREMENT = 1;
	DELETE FROM ocun_attribute WHERE attribute_id > 0;
	ALTER TABLE ocun_attribute_description AUTO_INCREMENT = 1;
	DELETE FROM ocun_attribute_description WHERE attribute_id > 0;
	ALTER TABLE ocun_attribute_group AUTO_INCREMENT = 1;
	DELETE FROM ocun_attribute_group WHERE attribute_group_id > 0;
	ALTER TABLE ocun_attribute_group_description AUTO_INCREMENT = 1;
	DELETE FROM ocun_attribute_group_description WHERE attribute_group_id > 0;






# category
DELETE FROM `ocun_demo1category` WHERE category_id > 0;
DELETE FROM `ocun_demo1category_description` WHERE category_id > 0;
DELETE FROM `ocun_demo1category_to_layout` WHERE category_id > 0;
DELETE FROM `ocun_demo1category_to_store` WHERE category_id > 0;
DELETE FROM `ocun_demo1category_path` WHERE category_id > 0;

# lazada excel
	SELECT a.product_id, a.name as '*Product Name', a.description as 'Product Description*', concat('http://beechinheong.com/image/',b.image) as 'Product Image 1*', b.model, b.price as '*Price', 'Bee Chin Heong' as '*Brand',b.quantity as '*Quantity', b.weight as '*Package Weight (kg)', b.length as '*Package Dimensions (cm)-Length (cm)', b.width as '*Package Dimensions (cm)-Width (cm)', b.height as '*Package Dimensions (cm)-Height (cm)' FROM `ocun_product_description` a INNER JOIN ocun_product b ON a.product_id = b.product_id  WHERE a.language_id = 2 and b.quantity != 0  

# Shopee
	SELECT a.product_id,c.category_id as 'Category', a.name as 'Product Name', a.description as 'Product Description', concat('http://beechinheong.com/image/',b.image) as 'Cover image', b.model as 'SKU', b.price as 'Price',b.quantity as 'Stock', b.weight as 'Weight' FROM ocun_product_description a INNER JOIN ocun_product b ON a.product_id = b.product_id INNER JOIN ocun_product_to_category c ON a.product_id = c.product_id WHERE a.language_id = 2 and b.quantity != 0
