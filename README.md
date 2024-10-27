
# Bike Rental CRM Project

This project is a **Bike Rental CRM** application developed using Salesforce to streamline and automate the bike rental process. The application includes features for managing customers, bike bookings, billing, and automated reminders for overdue payments, providing an efficient solution for bike rental businesses.

## Objectives

The project aims to achieve the following business goals:
- Automate the bike rental process to minimize manual work.
- Track and manage customer rental history, booking information, and billing.
- Provide reminders for overdue payments to ensure timely collection.
- Generate reports on bike rentals, vehicle usage, and customer data for better decision-making.

### Specific Outcomes
- Automated billing calculations based on rental duration and payment status.
- Easy management of customer, bike, and booking data.
- Implementation of reminders for overdue payments.
- Efficient tracking of payment statuses and rental fees.

## Salesforce Key Features and Concepts Utilized

- **Objects and Relationships**: Custom objects for **Customers**, **Bookings**, **Bikes**, and **Billing**.
- **Automated Processes**: Record-Triggered Flows, Scheduled Apex for payment reminders, and Screen Flows for customer registration and bike booking.
- **Formula Fields**: Used to calculate total rental days and amounts.
- **Validation Rules**: Ensuring data accuracy, such as valid rental periods and non-negative mileage.
- **Security**: Role-based access control for different users in the system.

## Apex Code

### Schedulable Class for Payment Reminder
## **Validation Rules**

### **Customer_Main__c Object:**
1. **Email Format Validator**: Ensures that the Email__c field contains a valid email format.
2. **Phone Number Validator**: Ensures that the Phone_Number__c contains only numeric values.

### **Booking__c Object**
1. **End Date Validator**: Ensures that the `End_Date__c` cannot be before the `Start_Date__c`.
2. **Payment Status Validator**: Ensures that the `Payment_Status__c` cannot be "Paid" unless a `Payment_Date__c` is provided.
3. **Booking Date Validator**: Ensures that the `Booking_Date__c` is not in the future.

### **Bike__c Object**
1. **Mileage Validator**: Ensures that `Mileage__c` cannot be negative.
2. **Rental Price Validator**: Ensures that `Rental_Price_per_Day__c` is greater than zero.

### **Billing__c Object**
1. **Payment Date Validator**: Ensures that the `Payment_Date__c` cannot be before the `Booking_Date__c`.
2. **Total Amount Validator**: Ensures that `Total_Rental_Amount_Input_c__c` is greater than zero.
3. **Payment Status Validator**: Ensures that the `Payment_Status__c` cannot be "Paid" if `Payment_Date__c` is empty.

## **Testing and Validation**

The project has been thoroughly tested through:
- **Unit Testing**: Apex classes and triggers have been unit tested to ensure functionality.
- **User Interface Testing**: Manual and automated tests have been conducted on the UI to ensure smooth customer interactions, including the registration and booking flows.

## **Key Scenarios Addressed by Salesforce**

- Efficient handling of customer data through Lookup fields and custom objects.
- Automated billing calculation based on rental durations and payment statuses.
- Notifications sent automatically to customers when a payment is overdue.
- Streamlined process for renting bikes, updating vehicle status, and returning bikes, reducing administrative effort.


## **Documentation**

For a detailed description of the project, including objectives, key features, and testing, refer to the project documentation:
📝 [Project Documentation](https://docs.google.com/document/d/1TyrPFRIoOUUMTyI9OVQoiTj7Tw0UHjPtWvVJWdfftco/edit?usp=sharing)

## **Video Link**
For a detailed demonstration video click here: 🎥 [Video Demo](https://drive.google.com/file/d/1OERC1AkxQZA68Wwx7L8YcdI3GKTH4C52/view?usp=sharing)

---

Feel free to explore the project and contribute if you'd like to enhance its features or improve the functionality!

---
