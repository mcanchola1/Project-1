# Team 8 Mist 4610 Group Project 1

## Team Name: 
47114 Group 8 

## Team Members:

1. Arnav Gupta [@ArnavGupta](https://www.github.com/akg93611)
2. Ainsley Myers [@AinsleyMyers](https://www.github.com/anm00752)
3. Caroline Pitfield [@CarolinePitfield](https://www.github.com/cgpitfield)
4. Melanie Canchola [@MelanieCanchola](https://www.github.com/mcanchola1)

## Problem Description:
The `al_Group_47114_G8` database is designed for managing a movie theater's operations, 
including movie showings, customer transactions, concessions, employee shifts, and loyalty programs. 
This database allows managers to gain insights into sales, customer behavior, and employee performance.

## Data Model:

Explanation of the Data Model:

Our model is based on the structure of a movie theater. The entity movies holds all of the movies that are played at our theater. It organizes many aspects of the movie like the title, genre, and duration. There are many reviews made by customers, connecting reviews to movies in a one to many relationship. The entity reviews holds the rating and description from the customer. 

Since each customer can make many reviews, there is another one to many relationship from customers to reviews. The customers entity holds each customer’s name, contact information, and birth date. The customers can also choose to opt in for a loyalty program, connected by a one to many relationship since each loyalty program belongs to one customer. This holds their points balance and tier for different rewards at our theater.

The movies entity is also connected to showtimes, since each movie can be played at a different showtime. The showtimes entity connects to auditoriums in a many to many relationship since each auditorium can have many showtimes and each showtime can have a different auditorium. The middle entity is auditorium time, which identifies the specific auditorium for each specific showtime.

The tickets entity holds the seat number, price, purchase date, and multiple foreign keys. The entity is connected to showtimes to assign each showtime to a specific ticket. Tickets also connects to transactions in a one to many relationship since many tickets can be purchased in each transaction. Many concessions can also be in each transaction, connecting concessions in a one to many relationship. Concessions holds the item, price, and stock of each food item. 

Transactions are processed by an employee, connecting in a one to many relationship. The entity employees holds their name, role, and salary. Each employee can work different shifts, shown in a one to many relationship. Shifts holds the start and end time, date, and which employee works it.
![image](https://github.com/user-attachments/assets/39ac3850-0284-4fe2-a28d-6127e867860d)


## Data Dictionary
<img width="634" alt="Movies" src="https://github.com/user-attachments/assets/91c5752a-91d4-4085-90de-8476b8202a6e" />
<img width="637" alt="showtimes" src="https://github.com/user-attachments/assets/75ecc185-6ad5-4194-a7f0-6cb397d847d7" />
<img width="635" alt="auditoriums" src="https://github.com/user-attachments/assets/e629a979-641f-4651-ba48-a208018358a3" />
<img width="636" alt="customers" src="https://github.com/user-attachments/assets/0141b281-5acd-41ee-906e-bc8467a7321c" />
<img width="637" alt="LP" src="https://github.com/user-attachments/assets/2bed1298-540a-4e29-a4e5-7f680c921f7a" />
<img width="636" alt="ticks" src="https://github.com/user-attachments/assets/06d0c931-bee6-4a39-a831-7b4d2be67d60" />
<img width="637" alt="concession" src="https://github.com/user-attachments/assets/155ca329-63ef-4a5c-81ac-c5c055b13f07" />
<img width="638" alt="transactions" src="https://github.com/user-attachments/assets/d9dd1427-c1db-4115-9496-a29f76caa1e8" />
<img width="634" alt="employees" src="https://github.com/user-attachments/assets/d1c7604c-4054-4775-92ac-987a1563897f" />
<img width="636" alt="Shfits" src="https://github.com/user-attachments/assets/ce278efa-c332-4685-9937-b73a97a6c0c3" />
<img width="637" alt="Reviews" src="https://github.com/user-attachments/assets/237e929b-0b34-4a18-ae2a-70bc769cc123" />
<img width="650" alt="AT" src="https://github.com/user-attachments/assets/b0517a70-3bba-43e9-940f-4e9ed0aa2673" />

## **SQL Queries for Managerial Insights**

![image](https://github.com/user-attachments/assets/4ed8af12-89c3-4bb4-b0b3-b74224524131)

### **Simple Queries:**

### 1. **Find the total number of customers in the loyalty program**

```sql
SELECT COUNT(Loyalty_ID) FROM Loyalty_Program;
```
![Screenshot 2025-03-20 115103](https://github.com/user-attachments/assets/225e6493-cd7c-425a-a7ba-8fc365e10733)

**Justification:**

- Helps managers assess the adoption of the loyalty program and gauge customer retention.

### 2. **How many movies are available for each genre?**

```sql
SELECT Genre, COUNT(*) AS movie_count FROM Movies GROUP BY Genre ORDER BY movie_count DESC;
```
![Screenshot 2025-03-20 114652](https://github.com/user-attachments/assets/a3a41b04-0ea0-4ce5-93bd-05fcab093bf9)

**Justification:**

- Assists in ensuring a diverse selection of movies across different genres.

### 3. **Find the number of reviews each movie has received**

```sql
SELECT M.Title, COUNT(R.Review_ID) AS Review_Count FROM Movies M
JOIN Reviews R ON M.Movie_ID = R.Movies_Movie_ID
GROUP BY M.Title ORDER BY Review_Count DESC;
```
![Screenshot 2025-03-20 115202](https://github.com/user-attachments/assets/6f63d6ca-0a8e-44c8-a598-bf8bebb0f4e3)

**Justification:**

- Allows managers to see which movies engage audiences the most.

### 4. **Get the number of tickets sold per showtime**

```sql
SELECT S.Showtime_ID, COUNT(T.Ticket_ID) AS Tickets_Sold FROM Showtimes S
JOIN Tickets T ON S.Showtime_ID = T.Showtimes_Showtime_ID
GROUP BY S.Showtime_ID ORDER BY Tickets_Sold DESC;
```
![Screenshot 2025-03-20 115302](https://github.com/user-attachments/assets/35f957ec-6c41-4aae-83f5-eb7982b2a5ff)

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
![Screenshot 2025-03-20 115347](https://github.com/user-attachments/assets/9eda6d50-9959-4162-838a-a937fabbeeaa)

**Justification:**

- Assists in tracking down staff responsible for a shift if an issue arises.

### 6. **Get the average rating for each movie, ordered from best to worst**

```sql
SELECT M.Title, AVG(R.Rating) AS 'Avg Rating' FROM Movies M
JOIN Reviews R ON M.Movie_ID = R.Movies_Movie_ID
GROUP BY M.Title ORDER BY AVG(R.Rating) DESC;
```
![image](https://github.com/user-attachments/assets/3aa3de3c-12bc-4444-9aee-c38679f4ff9d)

**Justification:**

- Provides insights into audience preferences, allowing for better movie promotions.

### 7. **Find a list of the top-selling concessions items**

```sql
SELECT C.Item_Name, COUNT(T.Transaction_ID) AS 'Amount Sold'
FROM Concessions C
JOIN Transactions T ON C.Transactions_Transaction_ID = T.Transaction_ID
GROUP BY C.Item_Name ORDER BY COUNT(T.Transaction_ID) DESC;
```
![Screenshot 2025-03-20 115739](https://github.com/user-attachments/assets/54965805-6ead-4c9e-8f56-22b7eeda47ef)

**Justification:**

- Helps manage concession inventory and identify popular items.

### 8. **Top 5 highest-paying customers and their last purchase date**

```sql
SELECT First_Name, Last_Name, SUM(Total_Amount) AS Total_Spent, MAX(Date) AS Last_Purchase
FROM Customers JOIN Transactions t ON Customer_ID = Customers_Customer_ID
GROUP BY Customer_ID ORDER BY Total_Spent DESC LIMIT 5;
```
![image](https://github.com/user-attachments/assets/1be006df-3f95-424a-b1b3-8f47149b8682)

**Justification:**

- Identifies valuable customers for loyalty programs and exclusive promotions.

### 9. **Top 3 employees with the highest transaction performance**

```sql
SELECT First_Name, Last_Name, COUNT(Transaction_ID) AS Total_Transactions
FROM Employees JOIN Transactions ON Employees.Employee_ID = Transactions.Employees_Employee_ID
GROUP BY Employee_ID ORDER BY Total_Transactions DESC LIMIT 3;
```
![image](https://github.com/user-attachments/assets/5a450f99-5746-4e66-95e3-8a1ad3698052)

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

![image](https://github.com/user-attachments/assets/a89feb29-6da4-48e9-826e-8216988b6a15)


**Justification:**

- Helps in scheduling and pricing adjustments based on showtime occupancy rates.

---

## **Conclusion**
Name of the database: al_Group_47114_G8

This database provides an efficient way to manage theater operations, track employee performance, optimize scheduling, and enhance customer engagement. 
These queries serve as valuable tools for managerial decision-making and business strategy planning.


