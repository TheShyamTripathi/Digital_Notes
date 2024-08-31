It looks like there’s a small issue in your table creation syntax, specifically with the `PRIMARY KEY` constraint. The `PRIMARY KEY` should be separated as `PRIMARY KEY (Flight_NO)` or be part of the column definition with a space between `INT` and `PRIMARY KEY`. Here's the corrected version:

```sql
CREATE TABLE flight_info (
    Flight_NO INT PRIMARY KEY,
    Start VARCHAR(50),
    Destination VARCHAR(50),
    Fare FLOAT(10, 2),
    Total_Seat INT NOT NULL,
    Avail_Seat INT NOT NULL,
    Flight_date DATE
);
```

This will create the `flight_info` table with the specified columns and constraints.


Here's the simplified `PLANE_INFO` table with only the `Plane_ID`, `Plane_Model`, `Total_Seat`, and `Year_Manufactured` columns:

```sql
CREATE TABLE PLANE_INFO (
    Plane_ID INT PRIMARY KEY,         -- Unique identifier for each plane
    Plane_Model VARCHAR(100),         -- Model of the plane
    Total_Seat INT NOT NULL,          -- Total number of seats in the plane
    Year_Manufactured YEAR            -- Year the plane was manufactured
);
```

This table now contains only the necessary columns you specified.


To include a contact number in the `Customer_info` table, you can add a `Contact` column. Here’s the updated table creation statement:

```sql
CREATE TABLE Customer_info (
    Customer_id INT PRIMARY KEY,     -- Unique identifier for each customer
    Fname VARCHAR(50),               -- First name of the customer
    Lname VARCHAR(50),               -- Last name of the customer
    Booking_ID INT,                  -- Booking ID associated with the customer
    Contact VARCHAR(15)              -- Contact number of the customer
);
```

In this table:
- **Contact**: A column for storing the customer’s contact number, with a length of 15 characters (sufficient for most phone numbers). You can adjust the length based on your needs.



  Here’s the revised `Booking_info` table creation statement with a foreign key constraint linking `Flight_No` to `Flight_NO` in the `flight_info` table:

```sql
CREATE TABLE Booking_info (
    Booking_Id INT PRIMARY KEY,       -- Unique identifier for each booking
    Flight_No INT,                    -- Flight number for the booking
    No_of_seat INT,                  -- Number of seats booked
    FOREIGN KEY (Flight_No) REFERENCES flight_info(Flight_NO) -- Foreign key constraint
);
```

This statement creates the `Booking_info` table with the `Booking_Id` as the primary key and includes a foreign key constraint that links `Flight_No` to the `Flight_NO` column in the `flight_info` table.


ALTER TABLE Booking_info
ADD CONSTRAINT fk_plane
FOREIGN KEY (Plane_ID) REFERENCES PLANE_INFO(Plane_ID);

