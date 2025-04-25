CREATE DATABASE IF NOT EXISTS E_commerce;

USE E_commerce;
-- 1. brand
CREATE TABLE brand (
    brand_id INT AUTO_INCREMENT PRIMARY KEY,
    brand_name VARCHAR(100) NOT NULL,
    description TEXT
);

-- 2. product_category
CREATE TABLE product_category (
    category_id INT AUTO_INCREMENT PRIMARY KEY,
    category_name VARCHAR(100) NOT NULL,
    description TEXT
);

-- 3. product
CREATE TABLE product (
    product_id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(150) NOT NULL,
    brand_id INT,
    category_id INT,
    base_price DECIMAL(10,2),
    FOREIGN KEY (brand_id) REFERENCES brand(brand_id),
    FOREIGN KEY (category_id) REFERENCES product_category(category_id)
);

-- 4. product_image
CREATE TABLE product_image (
    image_id INT AUTO_INCREMENT PRIMARY KEY,
    product_id INT,
    url VARCHAR(255) NOT NULL,
    alt_text VARCHAR(150),
    FOREIGN KEY (product_id) REFERENCES product(product_id)
);

-- 5. color
CREATE TABLE color (
    color_id INT AUTO_INCREMENT PRIMARY KEY,
    color_name VARCHAR(50) NOT NULL,
    hex_code VARCHAR(7)
);

-- 6. size_category
CREATE TABLE size_category (
    size_cat_id INT AUTO_INCREMENT PRIMARY KEY,
    category_name VARCHAR(100) NOT NULL
);

-- 7. size_option
CREATE TABLE size_option (
    size_id INT AUTO_INCREMENT PRIMARY KEY,
    size_cat_id INT,
    size_label VARCHAR(20) NOT NULL,
    FOREIGN KEY (size_cat_id) REFERENCES size_category(size_cat_id)
);

-- 8. product_variation
CREATE TABLE product_variation (
    variation_id INT AUTO_INCREMENT PRIMARY KEY,
    product_id INT,
    color_id INT,
    size_id INT,
    FOREIGN KEY (product_id) REFERENCES product(product_id),
    FOREIGN KEY (color_id) REFERENCES color(color_id),
    FOREIGN KEY (size_id) REFERENCES size_option(size_id)
);

-- 9. product_item
CREATE TABLE product_item (
    item_id INT AUTO_INCREMENT PRIMARY KEY,
    product_id INT,
    variation_id INT,
    sku VARCHAR(50) UNIQUE,
    stock INT,
    price DECIMAL(10,2),
    FOREIGN KEY (product_id) REFERENCES product(product_id),
    FOREIGN KEY (variation_id) REFERENCES product_variation(variation_id)
);

-- 10. attribute_category
CREATE TABLE attribute_category (
    attr_cat_id INT AUTO_INCREMENT PRIMARY KEY,
    category_name VARCHAR(100) NOT NULL
);

-- 11. attribute_type
CREATE TABLE attribute_type (
    attribute_type_id INT AUTO_INCREMENT PRIMARY KEY,
    attr_cat_id INT,
    type_name VARCHAR(100) NOT NULL,
    data_type VARCHAR(50),
    FOREIGN KEY (attr_cat_id) REFERENCES attribute_category(attr_cat_id)
);

-- 12. product_attribute
CREATE TABLE product_attribute (
    attr_id INT AUTO_INCREMENT PRIMARY KEY,
    product_id INT,
    attribute_type_id INT,
    value TEXT,
    FOREIGN KEY (product_id) REFERENCES product(product_id),
    FOREIGN KEY (attribute_type_id) REFERENCES attribute_type(attribute_type_id)
);

-- Data Inserts
-- Combined Inserts for E-commerce Database

-- 1. Brands
INSERT INTO brand (brand_name, description) VALUES
('Nike', 'Sportswear brand'),
('Samsung', 'Electronics brand'),
('Adidas', 'Sportswear brand'),
('Sony', 'Electronics brand'),
('Apple', 'Electronics brand'),
('Puma', 'Sportswear brand'),
('LG', 'Electronics brand'),
('Under Armour', 'Sportswear brand'),
('Asus', 'Electronics brand'),
('Dell', 'Electronics brand'),
('HP', 'Electronics brand'),
('Lenovo', 'Electronics brand'),
('OnePlus', 'Electronics brand'),
('Motorola', 'Electronics brand'),
('Reebok', 'Sportswear brand'),
('Philips', 'Home appliances brand'),
('Panasonic', 'Home appliances brand'),
('Canon', 'Photography brand'),
('JBL', 'Audio equipment brand'),
('Beats', 'Audio equipment brand');

-- 2. Product Categories
INSERT INTO product_category (category_name, description) VALUES
('Clothing', 'Apparel items like shoes, shirts, etc.'),
('Phones', 'Mobile devices and smartphones'),
('Electronics', 'Electronics like TVs, laptops, etc.'),
('Home Appliances', 'Appliances for home use'),
('Photography', 'Photography equipment');

-- 3. Colors
INSERT INTO color (color_name, hex_code) VALUES
('Red', '#FF0000'),
('Black', '#000000'),
('Blue', '#0000FF'),
('Green', '#00FF00'),
('White', '#FFFFFF'),
('Yellow', '#FFFF00'),
('Gray', '#808080'),
('Orange', '#FFA500'),
('Purple', '#800080'),
('Pink', '#FFC0CB'),
('Teal', '#008080'),
('Navy', '#000080'),
('Maroon', '#800000'),
('Olive', '#808000'),
('Cyan', '#00FFFF'),
('Brown', '#A52A2A'),
('Gold', '#FFD700'),
('Silver', '#C0C0C0'),
('Lime', '#00FF00'),
('Indigo', '#4B0082');

-- 4. Size Categories
INSERT INTO size_category (category_name) VALUES
('Clothing Sizes'), ('Shoe Sizes'), ('Device Sizes');

-- 5. Size Options
INSERT INTO size_option (size_cat_id, size_label) VALUES
(1, 'S'), (1, 'M'), (1, 'L'), (1, 'XL'), (1, 'XXL'),
(2, '38'), (2, '40'), (2, '42'), (2, '44'), (2, '46'),
(3, '6.1'), (3, '6.7'), (3, '13'), (3, '15'), (3, '27'),
(3, '32'), (3, '40'), (3, '42'), (3, '50'), (3, '55');

-- 6. Attribute Categories
INSERT INTO attribute_category (category_name) VALUES
('Physical'), ('Technical');

-- 7. Attribute Types
INSERT INTO attribute_type (attr_cat_id, type_name, data_type) VALUES
(1, 'Weight', 'text'),
(2, 'Battery Life', 'text'),
(2, 'Usage Time', 'text'),
(2, 'Resolution', 'text'),
(2, 'Processor Speed', 'text'),
(2, 'Charging Time', 'text'),
(1, 'Material', 'text'),
(1, 'Waterproof', 'boolean'),
(1, 'Dimensions', 'text'),
(2, 'Bluetooth', 'boolean'),
(2, 'Operating System', 'text'),
(1, 'Color', 'text'),
(2, 'Camera', 'text'),
(2, 'Aperture', 'text'),
(2, 'Storage', 'text'),
(1, 'Fit Type', 'text'),
(1, 'Capacity', 'text'),
(2, 'Temperature Range', 'text'),
(2, 'Voltage', 'text'),
(2, 'Compatibility', 'text');

-- 8. Products
INSERT INTO product (name, brand_id, category_id, base_price) VALUES 
('Air Max 270', 1, 1, 120.00),  -- Clothing
('Galaxy S21', 2, 2, 799.99),  -- Phones
('Ultraboost Shoes', 3, 1, 180.00),  -- Clothing
('Bravia 4K TV', 4, 2, 950.00),  -- Electronics
('iPhone 14', 5, 2, 999.99),  -- Phones
('Running Shoes', 6, 1, 100.00),  -- Clothing
('Smart Fridge', 7, 4, 1300.00),  -- Home Appliances
('Compression Shirt', 8, 1, 55.00),  -- Clothing
('Gaming Laptop', 9, 2, 1500.00),  -- Electronics
('Inspiron 15', 10, 2, 700.00),  -- Electronics
('Pavilion Desktop', 11, 2, 850.00),  -- Electronics
('ThinkPad X1', 12, 2, 1200.00),  -- Electronics
('Nord 3', 13, 2, 450.00),  -- Phones
('Edge 30', 14, 2, 500.00),  -- Phones
('Nano X Trainers', 15, 1, 130.00),  -- Clothing
('Smart Toothbrush', 16, 4, 60.00),  -- Home Appliances
('Microwave Oven', 17, 4, 120.00),  -- Home Appliances
('EOS R10 Camera', 18, 5, 1150.00),  -- Photography
('Charge 4 Speaker', 19, 2, 150.00),  -- Electronics
('Beats Studio Buds', 20, 2, 160.00);  -- Electronics


-- 9. Product Images
INSERT INTO product_image (product_id, url, alt_text) VALUES
(1, 'airmax270.jpg', 'Nike Air Max 270'),
(2, 'galaxys21.jpg', 'Samsung Galaxy S21'),
(3, 'ultraboost.jpg', 'Adidas Ultraboost Shoes'),
(4, 'bravia4k.jpg', 'Sony Bravia 4K TV'),
(5, 'iphone14.jpg', 'Apple iPhone 14'),
(6, 'runningshoes.jpg', 'Puma Running Shoes'),
(7, 'smartfridge.jpg', 'LG Smart Fridge'),
(8, 'shirt.jpg', 'Under Armour Compression Shirt'),
(9, 'gaminglaptop.jpg', 'Asus Gaming Laptop'),
(10, 'inspiron.jpg', 'Dell Inspiron 15'),
(11, 'pavilion.jpg', 'HP Pavilion Desktop'),
(12, 'thinkpad.jpg', 'Lenovo ThinkPad X1'),
(13, 'nord3.jpg', 'OnePlus Nord 3'),
(14, 'edge30.jpg', 'Motorola Edge 30'),
(15, 'nanox.jpg', 'Reebok Nano X Trainers'),
(16, 'toothbrush.jpg', 'Philips Smart Toothbrush'),
(17, 'microwave.jpg', 'Panasonic Microwave Oven'),
(18, 'eosr10.jpg', 'Canon EOS R10'),
(19, 'charge4.jpg', 'JBL Charge 4'),
(20, 'beatsbuds.jpg', 'Beats Studio Buds');

-- 10. Product Variations
INSERT INTO product_variation (product_id, color_id, size_id) VALUES
(1, 1, 1), (2, 2, 2), (3, 3, 3), (4, 4, 4), (5, 5, 5),
(6, 6, 6), (7, 7, 7), (8, 8, 8), (9, 9, 9), (10, 10, 10),
(11, 11, 11), (12, 12, 12), (13, 13, 13), (14, 14, 14), (15, 15, 15),
(16, 16, 16), (17, 17, 17), (18, 18, 18), (19, 19, 19), (20, 20, 20);

-- 11. Product Items
INSERT INTO product_item (product_id, variation_id, sku, stock, price) VALUES
(1, 1, 'NIKE270-RED-42', 25, 120.00),
(2, 2, 'SGS21-BLK-6.1', 50, 799.99),
(3, 3, 'ADIUB-BLU-40', 40, 180.00),
(4, 4, 'SNY4K-GRN-32', 10, 950.00),
(5, 5, 'APL14-WHT-6.7', 35, 999.99),
(6, 6, 'PUMA-YEL-42', 28, 100.00),
(7, 7, 'LGF-GRY-32', 15, 1300.00),
(8, 8, 'UA-BLK-M', 60, 55.00),
(9, 9, 'ASUS-GAM-27', 8, 1500.00),
(10, 10, 'DEL-INSP-27', 12, 700.00),
(11, 11, 'HP-PAV-27', 11, 850.00),
(12, 12, 'LNV-TX1-27', 9, 1200.00),
(13, 13, 'OP-N3-6.1', 40, 450.00),
(14, 14, 'MOTO-E30-6.1', 30, 500.00),
(15, 15, 'RBK-NX-40', 25, 130.00),
(16, 16, 'PHP-TOOTH', 70, 60.00),
(17, 17, 'PAN-MICRO', 40, 120.00),
(18, 18, 'CANNON-EOSR', 5, 1150.00),
(19, 19, 'JBL-C4', 20, 150.00),
(20, 20, 'BEATS-BUDS', 18, 160.00);

-- 12. Product Attributes
INSERT INTO product_attribute (product_id, attribute_type_id, value) VALUES
(1, 1, '350g'), (2, 2, '18h battery'), (3, 3, '8h life'),
(4, 4, '4K UHD'), (5, 5, '3.2GHz'), (6, 6, '1.5h charge'),
(7, 7, 'Steel body'), (8, 8, 'Sweat resistant'),
(9, 9, '15x10x1'), (10, 10, 'Yes'), (11, 11, 'Windows 11'),
(12, 12, 'Black'), (13, 13, 'Triple lens'), (14, 14, 'f/1.8'),
(15, 15, '512GB SSD'), (16, 16, 'Slim fit'), (17, 17, '100kg capacity'),
(18, 18, '0-40°C'), (19, 19, '220V'), (20, 20, 'Android');



