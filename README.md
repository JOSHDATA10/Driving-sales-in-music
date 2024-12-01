# 🎵 Chinook Music Database Analysis

## Table of Contents
- [Introduction](#introduction)
- [Objective](#objective)
- [Data Source](#data-source)
- [Tools Used](#tools-used)
- [Data Analysis Process](#data-analysis-process)
- [Key Insights](#key-insights)
- [Conclusion](#conclusion)
- [Recommendations](#recommendations)
- [Sample SQL Query](#sample-sql-query)

---

## Introduction
This project explores the **Chinook Music Database**, a dataset commonly used for SQL learning and practice. It contains information about customers, invoices, tracks, artists, and genres, making it ideal for analyzing music sales and customer behavior.

---

## Objective
The goals of this analysis are:
1. Identify the top-performing artists, genres, and customer segments.
2. Explore trends in yearly sales and customer purchasing patterns.
3. Provide actionable insights for better decision-making in music product marketing.

---

## Data Source
The analysis was conducted on the Chinook SQLite database, which consists of multiple tables linked by unique keys. Key data elements include:
- Customer data
- Invoice and transaction data
- Music track, album, and genre details
- Artist and employee data

---

## Tools Used
- **SQLite**: Database querying and data extraction.
- **Excel**: Additional data cleaning.
- **Power BI**: Data visualization and reporting.

---

## Data Analysis Process
1. **Database Exploration**: Querying tables to understand structure and relationships.
2. **Data Cleaning**: Removing duplicates, handling nulls, and standardizing formats.
3. **Metrics Creation**: Generating KPIs and calculated columns.
4. **Visualization**: Creating dashboards for insights.

## Key Insights
1. Top Customers and Regions
The USA had the highest sales and the largest number of high-value customers.
Most top customers are concentrated in North America and Europe.
2. Top Artists and Tracks
Iron Maiden emerged as the artist with the highest revenue and album sales, despite a decline in 2011.
Other top-performing artists include Led Zeppelin and U2.
3. Top Genres
Rock dominated with the highest track count and revenue contribution.
Pop and Jazz followed as the second and third most popular genres.
4. Yearly Sales Trends
2010 recorded the highest sales overall, driven by rock releases.
2009 had the lowest sales due to fewer album releases and declining interest in rock music.
5. Customer Preferences
Customers preferred purchasing full albums over single tracks, with album bundles driving revenue.


## Conclusion
The Chinook Music Database provides valuable insights into customer preferences, sales trends, and music popularity. Key takeaways include:

Rock is the most profitable genre, with Iron Maiden leading despite a decline in recent years.
The USA is the dominant region for sales, making it a priority target for marketing efforts.
Diversifying genres and focusing on new artists can drive future growth.


## Recommendations
Targeted Marketing: Focus on North American and European customers who contribute the most revenue.
Genre Diversification: Invest in promoting Pop and Jazz to balance dependency on Rock.
Digital Distribution: Encourage customers to purchase digital bundles and subscriptions for consistent revenue.
Track New Artists: Identify and promote up-and-coming artists in Rock and Pop to maintain dominance in these genres.



---

## Sample SQL Query
```sql
SELECT 
    ar.Name AS ArtistName, 
    SUM(inv.UnitPrice * inv.Quantity) AS TotalSales, 
    iv.InvoiceDate, 
    c.FirstName || ' ' || c.LastName AS FullName, 
    COUNT(DISTINCT iv.InvoiceId) AS TotalPurchases, 
    AVG(inv.UnitPrice * inv.Quantity) AS AvgTotalSales, 
    MAX(iv.InvoiceDate) AS LastPurchaseDate,
    c.CustomerId,
    STRFTIME('%Y', iv.InvoiceDate) AS Year, 
    COUNT(t.TrackId) AS TracksSold,
    RANK() OVER (PARTITION BY STRFTIME('%Y', iv.InvoiceDate) ORDER BY COUNT(t.TrackId) DESC) AS Rank, 
    g.Name AS GenreName
FROM artists AS ar
LEFT JOIN albums AS a ON ar.ArtistId = a.ArtistId
LEFT JOIN tracks AS t ON a.AlbumId = t.AlbumId
LEFT JOIN invoice_items AS inv ON t.TrackId = inv.TrackId
LEFT JOIN invoices AS iv ON inv.InvoiceId = iv.InvoiceId
RIGHT JOIN customers AS c ON c.CustomerId = iv.CustomerId
RIGHT JOIN genres AS g ON t.GenreId = g.GenreId
GROUP BY GenreName, FullName
ORDER BY TracksSold, TotalSales DESC; ```

---
## Key Insights
1. Top Customers and Regions
The USA had the highest sales and the largest number of high-value customers.
Most top customers are concentrated in North America and Europe.
2. Top Artists and Tracks
Iron Maiden emerged as the artist with the highest revenue and album sales, despite a decline in 2011.
Other top-performing artists include Led Zeppelin and U2.
3. Top Genres
Rock dominated with the highest track count and revenue contribution.
Pop and Jazz followed as the second and third most popular genres.
4. Yearly Sales Trends
2010 recorded the highest sales overall, driven by rock releases.
2009 had the lowest sales due to fewer album releases and declining interest in rock music.
5. Customer Preferences
Customers preferred purchasing full albums over single tracks, with album bundles driving revenue.


## Conclusion
The Chinook Music Database provides valuable insights into customer preferences, sales trends, and music popularity. Key takeaways include:

Rock is the most profitable genre, with Iron Maiden leading despite a decline in recent years.
The USA is the dominant region for sales, making it a priority target for marketing efforts.
Diversifying genres and focusing on new artists can drive future growth.


## Recommendations
Targeted Marketing: Focus on North American and European customers who contribute the most revenue.
Genre Diversification: Invest in promoting Pop and Jazz to balance dependency on Rock.
Digital Distribution: Encourage customers to purchase digital bundles and subscriptions for consistent revenue.
Track New Artists: Identify and promote up-and-coming artists in Rock and Pop to maintain dominance in these genres.

