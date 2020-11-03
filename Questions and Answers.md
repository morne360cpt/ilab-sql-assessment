# ILab SQL Assessment

## Questions and Answers

1. Display a list of all employees sorted according to Last Name in ascending order i.e. A-Z.

    ```
    SELECT * FROM Employees
	    ORDER BY LastName ASC;
    ```

2. Display a list of all suppliers from France who but not from Paris.

    ```
    SELECT * FROM Suppliers
        WHERE Country = "France" AND City <> "Paris";
    ```

3. Display all Suppliers whose SupplierName name begins with N.

    ```
    SELECT * FROM Suppliers
        WHERE SupplierName Like "N%";
    ```

4. Display a list of each country where customers are located (N.B. Your list should not contain two of the same values).

    ```
    SELECT DISTINCT Country FROM Customers
        ORDER BY Country ASC;
    ```

5. Display a list of all Customers and their order dates that made orders after 1996. Your result should look as follows:

    ```
    SELECT Orders.OrderID, Orders.OrderDate, Customers.CustomerName FROM Orders, Customers
        WHERE Orders.OrderDate > "1996/12/31";
    ```

6. Display each Order and Product ID sold as well as the total sales for each product (sales = productprice*quantity). Hint: You will have to join the Products table to get the price of each product. Your result should look as follows…

    ``` 
    SELECT OrderDetails.OrderID, OrderDetails.ProductID, (Products.Price * OrderDetails.Quantity) AS "Sales"
        FROM OrderDetails
        JOIN Products ON OrderDetails.ProductID=Products.ProductID;
    ```

7. Edit your previous query to display the Total Sales for each order. Note that orders may contain multiple products sold however we want to display the sum of all the sales for each order. Your result should look as follows…

    ``` 
    SELECT OrderDetails.OrderID, SUM(Products.Price * OrderDetails.Quantity) AS "Sales"
        FROM OrderDetails
        JOIN Products ON OrderDetails.ProductID=Products.ProductID
        GROUP BY OrderDetails.OrderID;
    ```

8. Edit your previous query to display all Order ID's as well as their Total Sales where the Total Sales for the whole order is greater than 10000.

    ```
    SELECT OrderDetails.OrderID, SUM(Products.Price * OrderDetails.Quantity) AS "Sales"
        FROM OrderDetails
        JOIN Products ON OrderDetails.ProductID=Products.ProductID
        GROUP BY OrderDetails.OrderID = ANY
        (SELECT Sales FROM OrderDetails WHERE Sales > 1000);
    ````

9. Select all order IDs that sold Products with IDs 19 and 35 on the same order i.e. for each order listed, it needs to contain product ID 19 and product ID 35. N.B we’re just looking for the OrderID to be returned. HINT: You can use a sub-query within your query.

    ```
    Select OrderID
        FROM OrderDetails
        WHERE ProductID = 19 AND 35;
    ```

10. Write a query to list all Employees as well as how many orders they have sold even if they have not made any orders and order the result by number of orders. Your list should like the below diagram…

    ```
    SELECT EmployeeID, COUNT(OrderID) AS "Orders"  
        FROM Orders
        GROUP BY EmployeeID
        HAVING COUNT(OrderID) >= 0
        ORDER BY COUNT(OrderID) ASC;
    ```
