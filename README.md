# Задачи, SQL-запросы:

1. Посчитай, сколько пользователей зарегистрировано в системе. Это таблица user_model. В результате выведи только количество пользователей

SELECT COUNT (Id) FROM user_model;

2. Добавь три новых разных продукта в таблицу product_model.

INSERT INTO product_model VALUES(114,'Курица гриль',200,1,'кг',13), (115,'Говядина',400,1,'кг',13),(116,'Свинина',400,1,'кг',13);

3. Посчитай количество продуктов в каждой категории и вывести id только тех категорий, в которых количество продуктов больше пяти. Это таблица product_model. Результат отсортируй в порядке возрастания количества продуктов.

SELECT "categoryId",  COUNT ( "categoryId" ) as productsCount   FROM product_model
GROUP BY ( "categoryId" )  HAVING COUNT ( "categoryId" ) >5  ORDER BY( "categoryId" ) ASC;

4. В приложение хотят добавить фичу — возможность вносить правки в заказы. Сработает только с теми заказами, где:
* стоимость доставки (deliveryPrice) больше 500,
* стоит статус «заказ формируется» или «заказ в доставке».
Напиши запрос, который будет выводить в системе id всех заказов и возможность внести правки. Назови эту колонку update_order. Если статус заказа позволяет вносить изменения, то в колонку update_order нужно вывести yes. Если правки внести нельзя — вывести no. 

SELECT id,
       CASE
           WHEN ("deliveryPrice") > 500 AND status  <= 1  THEN 'yes' 
           WHEN ("deliveryPrice") <= 500 OR status  = 2   THEN 'no' 
       END AS update_order
FROM order_model;

5. Выведи информацию о продуктах, цена которых находится в диапазоне от 200 до 500. Информация по каждому продукту включает: название продукта, цену, название категории, к которой он относится.

SELECT i.name, i.price, c.name FROM product_model AS i INNER JOIN category_model AS c ON i."categoryId" = c.id WHERE i.price BETWEEN 200 AND 500;

6. Для каждой карточки выведи ее название и количество продуктов (productsCount) для этой карточки. Результат отсортируй по названию карточки.

SELECT t.name, SUM (p."productsCount") FROM card_model AS t LEFT OUTER JOIN  kit_model AS p ON p."cardId" = t.id GROUP BY t.name ORDER BY  t.name ASC;

Автор: Клочков Сергей 