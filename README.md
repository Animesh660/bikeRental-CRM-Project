# bikeRental-CRM-Project
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
```java
public class RemindUnpaidBookings implements Schedulable {
    public void execute(SchedulableContext sc) {
        Date targetDate = Date.today().addDays(-3);
        List<Bike_Booking__c> unpaidBookings = [
            SELECT Id, Booking_ID__c, Customer_ID__r.Email__c, Customer_ID__r.Name, Payment_Status__c, End_Date__c
            FROM Bike_Booking__c
            WHERE End_Date__c <= :targetDate
              AND Payment_Status__c != 'Paid'
              AND Customer_ID__r.Email__c != null
        ];

        List<Messaging.SingleEmailMessage> emails = new List<Messaging.SingleEmailMessage>();
        for (Bike_Booking__c booking : unpaidBookings) {
            Messaging.SingleEmailMessage email = new Messaging.SingleEmailMessage();
            email.setToAddresses(new String[] { booking.Customer_ID__r.Email__c });
            email.setSubject('Payment Reminder for Your Bike Rental Booking #' + booking.Booking_ID__c);
            String body = 'Dear ' + booking.Customer_ID__r.Name + ',\n\n' +
                          'We hope you enjoyed your recent bike rental with us. Our records indicate that the payment for your booking #' + 
                          booking.Booking_ID__c + ' has not been received yet.\n\n' +
                          'Please make the payment at your earliest convenience to avoid any late fees or penalties.\n\n' +
                          'Thank you for choosing our services!\n\nBest regards,\nYour Bike Rental Team';
            email.setPlainTextBody(body);
            emails.add(email);
        }
        
        if (!emails.isEmpty()) {
            Messaging.sendEmail(emails);
        }
    }
}
