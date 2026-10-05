# Retail Performance Overview with Power BI
## Overview  
This project is a Power BI dashboard designed to analyze retail sales and customer data and provide a clear overview of business performance. The dashboard focuses on sales, profitability, customers, products, regions, and sales trends through interactive visualizations and key performance indicators.

## Objectives

- Analyze overall retail sales performance.
- Evaluate total revenue and profit.
- Understand customer and order activity.
- Analyze product performance.
- Compare sales performance across regions.
- Evaluate average order value and return rate.
- Identify important trends and patterns in sales data.

## Dataset

The data for this project is sourced from the Kaggle dataset:

- **Dataset Link:** [Retail Dataset](https://www.kaggle.com/datasets/hyerdrac/retail-data)

## Tools & Technologies

- Microsoft Power BI
- DAX
- Power BI Data Modeling
- Power Query

 ## Dashboard Preview

![Retail Sales & Customer Analytics Dashboard](https://github.com/maketadickson/power-bi-sales_dashboard/blob/main/Dashboard.png)

## Key Insights

The dashboard was used to identify patterns and trends in revenue, profit, customers, orders, products, regions, and returns as follows:

- Revenue and profit vary across products and regions.
- Customer and order volumes provide insight into overall sales activity.
- Average order value helps measure the value generated per order.
- Product-level analysis highlights differences in revenue, profitability, and return rates.
- Regional analysis reveals differences in sales performance across locations.
- Monthly sales trends show how revenue changes over time.

## Dax Measures

- **Number of customers**      

```dax
//The function below counts the number of unique customers in the customers table.

 DISTINCTCOUNT(customers[customer_id])
```

- **Total Customers**    

 // The function  below counts the number of distinct customers associated with the orders in the current filter context.

```dax
CALCULATE(
    DISTINCTCOUNT(orders[customer_id]),
    TREATAS(
        VALUES(order_details[order_id]),
        orders[order_id]
    )
)
```

- **Total Orders**      

 // The function below counts the total number of unique orders.

```dax
DISTINCTCOUNT(order_details[order_id])
```

- **Target Orders**  

 // The function below creates an order target based on the previous year's orders. If there is no previous year value, it returns a default target of 15,000; otherwise, it increases the previous year's orders by 15%.

```dax
VAR LastYearOrder = 
                    CALCULATE([Total Orders], SAMEPERIODLASTYEAR(date_table[Date]))


RETURN
            IF(ISBLANK(LastYearOrder), 15000,
                                            LastYearOrder * 1.5
                                            )   
```

_**Average Order Value**  

 // The function below calculates the average revenue generated per order by dividing Total Revenue by Total Orders.
```dax
 DIVIDE([Total Revenue], [Total Orders])
```

- **Total Profit**  

 // The function below calculates the total profit by summing the profit from all order details.
```dax

SUM(order_details[profit])
```

- **Total Revenue**  

 // The function below calculates the total revenue by summing the net sales from all order details.
```dax

 SUM(order_details[net_sale])
```

- **Return Rate**     

 // The function below calculates the return rate by dividing the number of returned orders by the total number of orders.
```dax
DIVIDE(
    CALCULATE(
        COUNTROWS(order_details),
        order_details[is_returned] = 1
    ),
    COUNTROWS(order_details)
```

## Conclusion

This project demonstrates the use of Power BI, DAX, Power Query, and data modeling to transform retail sales and customer data into an interactive business intelligence dashboard and communicate meaningful insights from the data.


