# Ecommerce-Db

INSERT INTO product_category (category_name) VALUES 
('Clothing'),
('Electronics'),
('Home Accessories');

INSERT INTO color (color_name)
VALUES('Red'),
      ('Blue'),
      ('Green'),
      ('Black');

INSERT INTO product (name, brand, base_price, category_id) 
VALUES('T-Shirt', 'long-sleeve', 19.99, 1),
      ('Sneakers', 'Nike', 49.99, 1),
      ('Smartphone', 'Samsung', 699.99, 2),
      ('Headphones', 'Huawei', 199.99, 2),
      ('Cushion', 'Burbbery', 24.99, 3);


INSERT INTO product_image (product_id, image_url, is_primary)  
VALUES(1, '/images/tshirt_red.jpg', TRUE),
      (2, 'images/sneakers_black.jpg', TRUE),
      (3, 'images/headphones.jpg', TRUE),
      
INSERT INTO product_item (product_id, color_id, size, stock_quantity, price) VALUES 
(1, 1, 'M', 100, 19.99),  -- Adidas T-shirt
(1, 2, 'L', 50, 19.99),   -- Puma T-Shirt
(2, 3, '10', 30, 49.99),  -- Reeebok T-shirt
