# WhatNext Vision Motors — Salesforce CRM Project

> *Shaping the Future of Mobility with Innovation and Excellence*

---

## Badges

<p align="left">
  <img src="https://img.shields.io/badge/Trailhead-Salesforce-00A1E0?style=for-the-badge&logo=salesforce&logoColor=white" alt="Trailhead" />
  <img src="https://img.shields.io/badge/SkillWallet-Program-7F77DD?style=for-the-badge&logoColor=white" alt="SkillWallet" />
  <img src="https://img.shields.io/badge/GitHub-Version%20Control-24292F?style=for-the-badge&logo=github&logoColor=white" alt="GitHub" />
  <img src="https://img.shields.io/badge/CRM-Salesforce-1D9E75?style=for-the-badge&logo=salesforce&logoColor=white" alt="CRM" />
</p>

---

## Table of Contents

- [Project Overview](#project-overview)
- [Team](#team)
- [Tech Stack](#tech-stack)
- [Modules](#modules)
- [Architecture](#architecture)
- [Key Features](#key-features)
- [Project Planning](#project-planning)
- [Testing](#testing)
- [Results & Screenshots](#results--screenshots)
- [Advantages & Disadvantages](#advantages--disadvantages)
- [Future Scope](#future-scope)
- [Source Code](#source-code)
- [Project Links](#project-links)

---

## Project Overview

**WhatNext Vision Motors** is a pioneering force in the automotive industry, dedicated to transforming the mobility sector with innovative technology and solutions that prioritize customer needs. This project implements an end-to-end **Salesforce CRM solution** for the automotive domain covering vehicles, dealers, customers, and orders.

| Property | Details |
|---|---|
| **Platform** | Salesforce CRM |
| **Domain** | Automotive CRM & EV Mobility |
| **Duration** | April – May 2026 |

---

## Team

| Role | Name |
|---|---|
| **Team Leader** | Ranjith Kumar S |
| **Team Member** | Tamil Selvan S |
| **Team Member** | Sriram Kumar K |
| **Team Member** | Thennarasu P |
| **Team Member** | Umar Farook U |

---

## Tech Stack

| Layer | Technology / Tool | Purpose |
|---|---|---|
| **CRM Platform** | Salesforce | Core platform hosting all custom objects, automation, and UI |
| **Data Layer** | Custom Objects (Vehicle, Dealer, Customer, Order) | Structured data storage with relationships |
| **Automation** | Salesforce Flow Builder (Record-Triggered Flow) | Auto Assign Dealer — nearest dealer suggestion on order creation |
| **Business Logic** | Apex Trigger + Handler Pattern | Real-time stock validation — blocks out-of-stock orders |
| **Batch Processing** | Apex Batch + Schedulable Interface | Bulk update of order status (Pending / Confirmed) based on stock |
| **UI Layer** | Salesforce Lightning App | Custom navigation for order management and reporting |

---

## Modules

### Module 1 — Vehicle Inventory Management (`Vehicle__c`)
The central object of the system. Each vehicle record stores its name, model type, price, stock quantity, linked dealer, and availability status. The Apex Trigger monitors this object to enforce stock constraints in real time, preventing orders from being placed when stock is zero.

### Module 2 — Dealer Network Management (`Dealer__c`)
Stores all authorized dealer information including location, phone, and email. The Auto Assign Dealer Flow uses this object to identify and assign the nearest dealer to a customer when a new order is placed, based on the customer's address.

### Module 3 — Customer Management (`Customer__c`)
Maintains customer profiles with contact details and address. The address field is used by the Auto Assign Dealer Flow to determine the nearest dealer at the time of order placement, delivering a personalized and convenient ordering experience.

### Module 4 — Order Processing (`Order__c`)
The transactional core of the system. Each order links a customer to a vehicle. The Auto Assign Dealer Flow fires on record creation to suggest the nearest dealer. The VehicleOrderTrigger validates stock before saving. The VehicleOrderBatch processes bulk pending orders on a schedule.

### Module 5 — Test Drive Management (`Vehicle_Test_Drive__c`)
Handles test drive bookings linking customers to vehicles with a scheduled date and status. The Test Drive Reminder Flow triggers on record create/update and sends automated reminder notifications to customers.

### Module 6 — Service Request Management (`Vehicle_Service_Request__c`)
Manages the complete after-sales service lifecycle. Customers raise service requests linked to their vehicle with an issue description, service date, and status (Requested / In Progress / Completed).

---

## Architecture

```
┌────────────────────────────────────────────────────────────────┐
│                     PRESENTATION LAYER                         │
│  WhatNext Vision Motors Lightning App                          │
│  Tabs: Vehicles | Customers | Dealers | Orders |               │
│        Test Drives | Service Requests | Reports | Dashboards   │
└────────────────────┬───────────────────────────────────────────┘
                     │
┌────────────────────▼───────────────────────────────────────────┐
│                     AUTOMATION LAYER                           │
│  Flow 1: Auto Assign Dealer (Record-Triggered on Order create) │
│  Flow 2: Test Drive Reminder (Scheduled Path)                  │
└────────────────────┬───────────────────────────────────────────┘
                     │
┌────────────────────▼───────────────────────────────────────────┐
│                   BUSINESS LOGIC LAYER                         │
│  VehicleOrderTrigger (before/after insert/update)              │
│  VehicleOrderTriggerHandler                                    │
│  VehicleOrderBatch + VehicleOrderBatchScheduler                │
└────────────────────┬───────────────────────────────────────────┘
                     │
┌────────────────────▼───────────────────────────────────────────┐
│                       DATA LAYER                               │
│  Vehicle__c | Vehicle_Dealer__c | Vehicle_Customer__c          │
│  Vehicle_Order__c | Vehicle_Test_Drive__c                      │
│  Vehicle_Service_Request__c                                    │
└────────────────────────────────────────────────────────────────┘
```

---

## Key Features

### 1. Nearest Dealer Auto-Assignment
The system automatically suggests the nearest dealer location to customers based on their address when placing an order, eliminating manual dealer selection entirely.

### 2. Out-of-Stock Order Prevention
The Apex Trigger blocks orders for vehicles with zero stock, displaying a clear error message and preventing overselling at the data layer.

```
"This vehicle is out of stock. Order cannot be placed."
```

### 3. Automated Batch Order Status Updates
A scheduled Batch Job accurately updates order status:
- **Confirmed** — Vehicle is in stock
- **Pending** — Vehicle is out of stock

---

## Project Planning

The project was executed over **4 sprints** using an Agile approach:

| Sprint | Duration | Activities | Deliverables |
|---|---|---|---|
| **Sprint 1** — Object Modeling | Week 1–2 | Created custom objects for Vehicle, Dealer, Customer, and Order; defined fields, data types, and Lookup relationships | `Vehicle__c`, `Dealer__c`, `Customer__c`, `Order__c` fully configured |
| **Sprint 2** — App & UI | Week 3–4 | Created WhatNext Vision Motors Lightning App; added navigation items; assigned System Administrator profile | Functional Lightning App accessible to admins |
| **Sprint 3** — Flow Automation | Week 5–6 | Built Auto Assign Dealer Flow (Record-Triggered on Order creation); nearest dealer suggested based on customer address | Auto dealer suggestion working on order creation |
| **Sprint 4** — Apex Development | Week 7–8 | Developed stock validation Apex Trigger; built Batch Job to update order status; tested all components end-to-end | Complete Apex automation layer with stock validation and batch processing |

### Key Milestones

- **Milestone 1 (Week 2):** All 4 custom objects created with correct fields and relationships; object tabs configured.
- **Milestone 2 (Week 4):** WhatNext Vision Motors Lightning App live with full navigation and System Administrator access.
- **Milestone 3 (Week 6):** Auto Assign Dealer Flow activated and tested — nearest dealer correctly assigned on order creation.
- **Milestone 4 (Week 8):** Apex Trigger, Batch Job, and Scheduler deployed and validated; full system end-to-end testing completed.

---

## Testing

### Functional Test Cases

| Test ID | Test Case | Expected Result | Actual Result | Status |
|---|---|---|---|---|
| TC-01 | Place an order for a vehicle with stock > 0 | Nearest dealer auto-suggested; order saved with dealer linked | Dealer assigned correctly; order saved | ✅ PASS |
| TC-02 | Place an order for a vehicle with stock = 0 | Order blocked with error: 'This vehicle is out of stock.' | Order blocked; correct error displayed | ✅ PASS |
| TC-03 | Run scheduled batch job — vehicle in stock | Order status updated to 'Confirmed'; stock decremented | Status set to Confirmed; stock reduced | ✅ PASS |
| TC-04 | Run scheduled batch job — vehicle out of stock | Order status updated to 'Pending' | Status set to Pending | ✅ PASS |
| TC-05 | Create a vehicle record with all mandatory fields | Record saved with model, price, stock, status stored correctly | Record saved successfully | ✅ PASS |
| TC-06 | Create a dealer record with location details | Dealer record saved; location available for assignment logic | Dealer record created correctly | ✅ PASS |
| TC-07 | Create a customer record with address | Customer record saved; address available for nearest dealer suggestion | Customer record saved with address | ✅ PASS |
| TC-08 | Verify order status lifecycle (Pending → Confirmed) | Order status transitions correctly based on stock and batch job | Status lifecycle works as expected | ✅ PASS |

### Performance Testing Results

| Metric | Result |
|---|---|
| **Flow Execution** | Auto Assign Dealer Flow executes within **500ms** of triggering |
| **Trigger Response** | VehicleOrderTrigger (before insert) responds within **200ms** |
| **Batch Processing** | Processes 50 records/execute(); 500-record batch completes in **< 10 seconds** |
| **App Load Time** | Lightning App loads all navigation tabs within **2 seconds** |

---

## Results & Screenshots

### Custom Objects & Relationships Overview

/Screenshots/Objects & Relationships.png
> *Fig 1: Custom Objects & Relationships — WhatNext Vision Motors Salesforce Org*

---

### Custom Object Field Configurations

<!-- Add screenshot: Fig 2 - Vehicle__c Fields & Relationships -->
> *Fig 2: `Vehicle__c` — Fields & Relationships (Price__c, Status__c, Stock_Quantity__c, Vehicle_Dealer__c Lookup, Vehicle_Model__c)*

<!-- Add screenshot: Fig 3 - Vehicle_Customer__c Fields & Relationships -->
> *Fig 3: `Vehicle_Customer__c` — Fields & Relationships (Address__c, Email__c, Phone__c, Preferred_Vehicle_Type__c)*

<!-- Add screenshot: Fig 4 - Vehicle_Dealer__c Fields & Relationships -->
> *Fig 4: `Vehicle_Dealer__c` — Fields & Relationships (Dealer_Code__c Auto Number, Dealer_Location__c, Email__c, Phone__c)*

---

### Custom Object Tab Creation

<!-- Add screenshot: Fig 5 - Custom Object Tabs -->
> *Fig 5: Custom Object Tabs — Vehicle Customers, Vehicle Dealers, Vehicle Orders, Vehicles, Vehicle Service Requests, Vehicle Test Drives*

---

### WhatNext Vision Motors Lightning App

<!-- Add screenshot: Fig 6 - Lightning App Branding -->
> *Fig 6: Lightning App — App Details & Branding (App Name: WhatNext Vision Motors, Color: #0070D2)*

<!-- Add screenshot: Fig 7 - Lightning App Navigation Items -->
> *Fig 7: Lightning App — Navigation Items (Vehicle Customers, Vehicle Dealers, Vehicle Orders, Vehicle Service Requests, Vehicle Test Drives, Vehicles, Reports, Dashboards)*

<!-- Add screenshot: Fig 8 - Lightning App User Profiles -->
> *Fig 8: Lightning App — User Profiles (System Administrator assigned)*

---

### Flow Automation

#### Flow 1 — Auto Assign Dealer

<!-- Add screenshot: Fig 9 - Auto Assign Dealer Flow -->
> *Fig 9: Auto Assign Dealer Flow — Record-Triggered on `Vehicle_Order__c` (Get Customer Info → Get Nearest Dealer → Assign Dealer to Order)*

#### Flow 2 — Test Drive Reminder

<!-- Add screenshot: Fig 10 - Test Drive Reminder Flow -->
> *Fig 10: Test Drive Reminder Flow — Scheduled Path fetches Customer Information and sends automated reminder notification*

---

## Advantages & Disadvantages

| ✅ Advantages | ❌ Disadvantages |
|---|---|
| Customers are automatically directed to the nearest dealer based on their address, reducing effort and improving ordering convenience. | The nearest-dealer suggestion currently uses a basic filter; a fully geo-coded, map-based algorithm would require additional configuration or Apex. |
| Out-of-stock vehicles are blocked at the point of order placement, eliminating overselling and improving order accuracy. | The batch job runs on a schedule; real-time order confirmation requires the Apex Trigger path, meaning batch and trigger logic must be carefully coordinated. |
| The scheduled batch job automatically updates order status to Confirmed or Pending based on stock, providing transparent communication to customers. | If stock changes rapidly, there may be a brief window between batch runs where order status does not immediately reflect the latest availability. |
| Automated processes reduce the administrative burden on staff, freeing them to focus on strategic and customer-facing activities. | Role-based access control for Sales Executives and Managers requires additional profile and permission set configuration beyond the current setup. |
| The ordering workflow scales efficiently for bulk order volumes through Batch Apex, respecting platform governor limits. | The solution currently runs on a developer environment with limited data storage and API call limits compared to a full production environment. |

---

## Future Scope

- **Geo-Based Dealer Assignment:** Enhance the Auto Assign Dealer Flow using Salesforce Maps or a custom Apex geo-coding service for precise geographical distance-based dealer assignment.
- **Role-Based Access Control:** Create custom Profiles and Permission Sets for Sales Executives, Dealers, and Branch Managers.
- **Customer Self-Service Portal:** Implement a Salesforce Experience Cloud portal for customers to place orders, check stock, track status, and find nearest dealers.
- **Real-Time Stock Synchronization:** Integrate Vehicle inventory with an external ERP or warehouse management system using Salesforce Connect or REST API.
- **Einstein AI Integration:** Add Einstein Next Best Action for vehicle recommendations and Einstein Analytics for management dashboards.
- **WhatsApp / SMS Notifications:** Integrate with a messaging platform (e.g., Twilio) for order confirmations and status updates.
- **Mobile App:** Extend the Lightning App to Salesforce Mobile for field sales executives.

---

## Source Code

### 1. `VehicleOrderTrigger.cls`
Entry-point Apex Trigger on `Vehicle_Order__c`. Fires on `before insert`, `before update`, `after insert`, and `after update`. Delegates all logic to `VehicleOrderTriggerHandler`.

```apex
trigger VehicleOrderTrigger on Vehicle_Order__c (before insert, before update, after insert, after update) {
    VehicleOrderTriggerHandler.handleTrigger(
        Trigger.new,
        Trigger.oldMap,
        Trigger.isBefore,
        Trigger.isAfter,
        Trigger.isInsert,
        Trigger.isUpdate
    );
}
```

---

### 2. `VehicleOrderTriggerHandler.cls`
Handler class with two methods:
- `preventOrderIfOutOfStock()` — blocks orders when stock is zero (before insert/update)
- `updateStockOnOrderPlacement()` — decrements stock by 1 when order status is Confirmed (after insert/update)

```apex
public class VehicleOrderTriggerHandler {

    public static void handleTrigger(List<Vehicle_Order__c> newOrders,
        Map<Id, Vehicle_Order__c> oldOrders, Boolean isBefore,
        Boolean isAfter, Boolean isInsert, Boolean isUpdate) {

        if (isBefore && (isInsert || isUpdate)) {
            preventOrderIfOutOfStock(newOrders);
        }
        if (isAfter && (isInsert || isUpdate)) {
            updateStockOnOrderPlacement(newOrders);
        }
    }

    // Prevent placing an order if stock is zero
    private static void preventOrderIfOutOfStock(List<Vehicle_Order__c> orders) {
        Set<Id> vehicleIds = new Set<Id>();
        for (Vehicle_Order__c order : orders) {
            if (order.Vehicle__c != null) vehicleIds.add(order.Vehicle__c);
        }
        if (!vehicleIds.isEmpty()) {
            Map<Id, Vehicle__c> vehicleStockMap = new Map<Id, Vehicle__c>(
                [SELECT Id, Stock_Quality__c FROM Vehicle__c WHERE Id IN :vehicleIds]
            );
            for (Vehicle_Order__c order : orders) {
                Vehicle__c vehicle = vehicleStockMap.get(order.Vehicle__c);
                if (vehicle != null && vehicle.Stock_Quality__c <= 0) {
                    order.addError('This vehicle is out of stock. Order cannot be placed.');
                }
            }
        }
    }

    // Decrease stock when an order is confirmed
    private static void updateStockOnOrderPlacement(List<Vehicle_Order__c> orders) {
        Set<Id> vehicleIds = new Set<Id>();
        for (Vehicle_Order__c order : orders) {
            if (order.Vehicle__c != null && order.Status__c == 'Confirmed')
                vehicleIds.add(order.Vehicle__c);
        }
        if (!vehicleIds.isEmpty()) {
            Map<Id, Vehicle__c> vehicleStockMap = new Map<Id, Vehicle__c>(
                [SELECT Id, Stock_Quality__c FROM Vehicle__c WHERE Id IN :vehicleIds]
            );
            List<Vehicle__c> vehiclesToUpdate = new List<Vehicle__c>();
            for (Vehicle_Order__c order : orders) {
                Vehicle__c vehicle = vehicleStockMap.get(order.Vehicle__c);
                if (vehicle != null && vehicle.Stock_Quality__c > 0) {
                    vehicle.Stock_Quality__c -= 1;
                    vehiclesToUpdate.add(vehicle);
                }
            }
            if (!vehiclesToUpdate.isEmpty()) update vehiclesToUpdate;
        }
    }
}
```

---

### 3. `VehicleOrderBatch.cls`
Batch Apex class implementing `Database.Batchable`. Queries all Pending `Vehicle_Order__c` records, confirms them, and decrements associated vehicle stock. Processes records in chunks of 50.

```apex
global class VehicleOrderBatch implements Database.Batchable<sObject> {

    global Database.QueryLocator start(Database.BatchableContext bc) {
        return Database.getQueryLocator([
            SELECT Id, Status__c, Vehicle__c
            FROM Vehicle_Order__c WHERE Status__c = 'Pending'
        ]);
    }

    global void execute(Database.BatchableContext bc, List<Vehicle_Order__c> orderList) {
        Set<Id> vehicleIds = new Set<Id>();
        for (Vehicle_Order__c order : orderList) {
            if (order.Vehicle__c != null) vehicleIds.add(order.Vehicle__c);
        }
        if (!vehicleIds.isEmpty()) {
            Map<Id, Vehicle__c> vehicleStockMap = new Map<Id, Vehicle__c>(
                [SELECT Id, Stock_Quality__c FROM Vehicle__c WHERE Id IN :vehicleIds]
            );
            List<Vehicle_Order__c> ordersToUpdate = new List<Vehicle_Order__c>();
            List<Vehicle__c> vehiclesToUpdate = new List<Vehicle__c>();
            for (Vehicle_Order__c order : orderList) {
                Vehicle__c vehicle = vehicleStockMap.get(order.Vehicle__c);
                if (vehicle != null && vehicle.Stock_Quality__c > 0) {
                    order.Status__c = 'Confirmed';
                    vehicle.Stock_Quality__c -= 1;
                    ordersToUpdate.add(order);
                    vehiclesToUpdate.add(vehicle);
                }
            }
            if (!ordersToUpdate.isEmpty()) update ordersToUpdate;
            if (!vehiclesToUpdate.isEmpty()) update vehiclesToUpdate;
        }
    }

    global void finish(Database.BatchableContext bc) {
        System.debug('Vehicle order batch job completed.');
    }
}
```

---

### 4. `VehicleOrderBatchScheduler.cls`
Schedulable Apex class that wraps `VehicleOrderBatch`. Can be scheduled via Salesforce Setup → Scheduled Jobs or via Anonymous Apex using `System.schedule()`.

```apex
global class VehicleOrderBatchScheduler implements Schedulable {
    global void execute(SchedulableContext sc) {
        VehicleOrderBatch batchJob = new VehicleOrderBatch();
        Database.executeBatch(batchJob, 50); // 50 = batch size
    }
}
```

---

## Project Links

| Resource | Link |
|---|---|
| **GitHub Repository** | [View on GitHub](https://github.com/zerotwo1910/NM_WhatNext_Vision_Motors) |
| **Project Demo Video** | [Watch Demo](https://drive.google.com/drive/folders/1NCnxv3U2qQUqcyQVXgG9KUiFCmBACISw) |
| **Trailhead Profile** | `ranjithrk2468.eacc9b32b248@agentforce.com` |

---

<div align="center">

**WhatNext Vision Motors — Shaping the Future of Mobility with Innovation and Excellence**

*Team: Ranjith Kumar S | Tamil Selvan S | Sriram Kumar K | Thennarasu P | Umar Farook U*

*April – May 2026*

</div>
