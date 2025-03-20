# **Database README: al_Group_47114_G8**

## **Overview**

The `al_Group_47114_G8` database is designed for managing a movie theater's operations, 
including movie showings, customer transactions, concessions, employee shifts, and loyalty programs. 
This database allows managers to gain insights into sales, customer behavior, and employee performance.

## **Database Structure**

### **Main Tables:**

- **Movies**: Stores movie details (Title, Genre, Duration, Rating, Release Date, Distributor).
- **Showtimes**: Lists showtime details and links to movies and auditoriums.
- **Auditoriums**: Stores information about auditorium seat capacities and sound systems.
- **Customers**: Contains customer details, including loyalty program participation.
- **Loyalty\_Program**: Tracks customer loyalty points and rewards claimed.
- **Tickets**: Manages ticket sales and links transactions to showtimes.
- **Concessions**: Stores concession items and their sales transactions.
- **Transactions**: Records purchases of tickets and concessions.
- **Employees**: Stores employee details and links them to shifts and transactions.
- **Shifts**: Manages employee work schedules.
- **Reviews**: Stores customer ratings and reviews for movies.

## **SQL Queries for Managerial Insights**

### **Simple Queries:**

### 1. **Find the total number of customers in the loyalty program**

```sql
SELECT COUNT(Loyalty_ID) FROM Loyalty_Program;
```

**Justification:**

- Helps managers assess the adoption of the loyalty program and gauge customer retention.

### 2. **How many movies are available for each genre?**

```sql
SELECT Genre, COUNT(*) AS movie_count FROM Movies GROUP BY Genre ORDER BY movie_count DESC;
```

**Justification:**

- Assists in ensuring a diverse selection of movies across different genres.

### 3. **Find the number of reviews each movie has received**

```sql
SELECT M.Title, COUNT(R.Review_ID) AS Review_Count FROM Movies M
JOIN Reviews R ON M.Movie_ID = R.Movies_Movie_ID
GROUP BY M.Title ORDER BY Review_Count DESC;
```

**Justification:**

- Allows managers to see which movies engage audiences the most.

### 4. **Get the number of tickets sold per showtime**

```sql
SELECT S.Showtime_ID, COUNT(T.Ticket_ID) AS Tickets_Sold FROM Showtimes S
JOIN Tickets T ON S.Showtime_ID = T.Showtimes_Showtime_ID
GROUP BY S.Showtime_ID ORDER BY Tickets_Sold DESC;
```

**Justification:**

- Helps optimize movie scheduling based on demand.

---

### **Complex Queries:**

### 5. **Find employees working on a specific day**

```sql
SELECT E.First_Name, E.Last_Name FROM Employees E
JOIN Shifts S ON E.Employee_ID = S.Employees_Employee_ID
WHERE S.Date = '2024-10-08';
```

**Justification:**

- Assists in tracking down staff responsible for a shift if an issue arises.

### 6. **Get the average rating for each movie, ordered from best to worst**

```sql
SELECT M.Title, AVG(R.Rating) AS 'Avg Rating' FROM Movies M
JOIN Reviews R ON M.Movie_ID = R.Movies_Movie_ID
GROUP BY M.Title ORDER BY AVG(R.Rating) DESC;
```

**Justification:**

- Provides insights into audience preferences, allowing for better movie promotions.

### 7. **Find a list of the top-selling concessions items**

```sql
SELECT C.Item_Name, COUNT(T.Transaction_ID) AS 'Amount Sold'
FROM Concessions C
JOIN Transactions T ON C.Transactions_Transaction_ID = T.Transaction_ID
GROUP BY C.Item_Name ORDER BY COUNT(T.Transaction_ID) DESC;
```

**Justification:**

- Helps in managing concession inventory and identifying popular items.

### 8. **Top 5 highest-paying customers and their last purchase date**

```sql
SELECT First_Name, Last_Name, SUM(Total_Amount) AS Total_Spent, MAX(Date) AS Last_Purchase
FROM Customers JOIN Transactions t ON Customer_ID = Customers_Customer_ID
GROUP BY Customer_ID ORDER BY Total_Spent DESC LIMIT 5;
```

**Justification:**

- Identifies valuable customers for loyalty programs and exclusive promotions.

### 9. **Top 3 employees with the highest transaction performance**

```sql
SELECT First_Name, Last_Name, COUNT(Transaction_ID) AS Total_Transactions
FROM Employees JOIN Transactions ON Employees.Employee_ID = Transactions.Employees_Employee_ID
GROUP BY Employee_ID ORDER BY Total_Transactions DESC LIMIT 3;
```

**Justification:**

- Helps managers recognize top-performing employees for rewards or promotions.

### 10. **List all showtimes with auditorium details and ticket sales, showing only showtimes that are at least half full**

```sql
SELECT
    M.Title AS Movie_Title,
    S.Showtime_ID,
    A.Auditorium_ID,
    A.Seat_Capacity,
    COUNT(T.Ticket_ID) AS Tickets_Sold
FROM Showtimes S
JOIN Movies M ON S.Movies_Movie_ID = M.Movie_ID
JOIN Auditoriums A ON S.Auditoriums_Auditorium_ID = A.Auditorium_ID
JOIN Tickets T ON S.Showtime_ID = T.Showtimes_Showtime_ID
GROUP BY S.Showtime_ID
HAVING Tickets_Sold >= (A.Seat_Capacity / 2)
ORDER BY Tickets_Sold DESC;
```

**Justification:**

- Helps in scheduling and pricing adjustments based on showtime occupancy rates.

---

## **Conclusion**

This database provides an efficient way to manage theater operations, track employee performance, optimize scheduling, and enhance customer engagement. 
These queries serve as valuable tools for managerial decision-making and business strategy planning.


