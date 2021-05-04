

# Architectural Katas 2021 - Team Pentagram

This is the fastest friendship we have ever made, just a week ago we did not know each others and now we are 100% into this project. Just four passionate guys about software architecture.
### Members
- Amit Bhatnagar: [LinkedIn](https://www.linkedin.com/in/b-amit/)
- Ali Imran: [LinkedIn](https://www.linkedin.com/in/aliimran-ibm/)
- Haidar Hadi:[LinkedIn](https://www.linkedin.com/in/haidar/)
- Somenath Mukherjee: [LinkedIn](https://www.linkedin.com/in/somenathmukherjee/)


## Introduction

### Business Problem

### Assumptions

-   Phase one of the development efforts aims to ensure that response time for ticket creation is <1s for 99% of ticket creation requests
    
-   Phase two of the development efforts aims to ensure that error rate of sending the wrong Sysops will drop to 1%
    
-   Phase three of the development efforts aims to ensure that self help will be available for customers to support themselves.
    
-   Phase four of the development efforts aims to ensure that auto prediction of issues and intelligent routing of Sysops will occur for 20% of the cases.
    
-   The system must handle the current registered customers of 300k with 30% annual growth rate, average customer owns three products with warranties and averages three ticks creation per year per product. Peak times of load are around 9AM and 4PM.
    
-   The system must be 100% reliable in storing ticket information. Tickets are handled within one hour or arrival; reviewed and assigned.
    
-   Ticket loss must be reduced to zero.
    
-   Customer support department is available between 7AM and 8PM

## Use Case Analysis

### Actors

1.  **Administrator** user maintains the internals of the system
1.  **Customer** : purchase support service from Penultimate Electronics   
1.  **Experts** are assigned problem tickets and fix problems based on the ticket.
1.  **Manager** keeps track of problem ticket operations and receives operational and analytical reports    
1.  **Customer support agent**: for ticket creation over the phone
1.  The **System**
  
### Use Cases 
-   UC-1: Administrator performs CRUD operations via UI on the Sysops Squad experts and system internals such as supported product list.

-   UC-2: Administrator generates list of experts and their corresponding skillset, location, and availability
   
-   UC-3: Administrator manages all of the billing processing for customers using the system, corrections , updates etc. Bill generation is handled by the system.
   
-   UC-4: Administrator maintains static reference data (such as supported products, name- value pairs in the system, and so on)
    
-   UC-5: Customer registers for the Sysops Squad service, maintains their customer profile, support contracts, and billing information.
    
-   UC-6: Customer enter problem tickets into the system
    
-   UC-7: Customer fills out surveys after the work has been completed.
    
-   UC-8: Customer views billing history and statements through the system.
    
-   UC-9: The expert receives a ticket
    
-   UC-10: Experts searches the KB for related information
    
-   UC11: Experts update the ticket with status and notes once done fixing the customer’s problem.
    
-   UC-12: The System periodically generates reports (operational and analytical) and send them to the manager
    
-   UC-13: The System periodically bills customers
    
-   UC-14: Admin system handles batch updates of new products and contracts
    
-   UC-15: The System routes tickets   
   
### Quality Attribute Scenarios

- QAS-1: A request to create a ticket is generated by end users (customer or support representative) the system will respond with a confirmation that includes a ticket number in less than a second during peak hours. 
	- Customers should not experience a degradation in response time or the quality of service under the following situations:
		- A failure in the hardware, software or the application does.
		- Fluctuations in customer demands (peak hours)
		- Expected annual customer growth of 30%. Specifically, new customers should have similar experience with the quality of service as existing customers.
	- QA: Performance: response time, scalability and elasticity
	- UC: UC5, UC6, UC8
	
-   QAS-2: When a CRUD operation is performed by Administrator the system will respond in less than a second during normal business hours (8AM-5PM)
	- QA: Performance
	- UC: UC1
	
-   QAS-3: The system is available for ticket creation and for customer data 99.999% of the time
	- QA: Availability
	- UC: All
	
-   QAS-4: The system is available for ancillary activities: billing, survey, internal configuration 99.00% of the time.
	- QA: Availability
	- UC: All
	
-   QAS-5: All components of the system can be independently tested (unit level).
	- QA: Testability
    	- UC: All
    	
-   QAS-6: Integration test of all the components of the system is performed on a daily basis against a preset list of scenarios to reflect any abnormalities (bugs/defects), individual components performance and general system performance.
	- QA: Testability
	- UC: All
	
-   QAS-7: The system must maintain backward compatibility and level of decoupling so that a change in one component does impact the rest of the system. For example, the ticket creation component can be deployed independently to the server without impacting the rest of the system.
	- QA: Modifiability: configuration changes and maintainability
	- UC: All
  

### Constraints

-   CON-1: The system must support a load of six tpm (transactions per minute) test must run at 60 tpm to accomodate for scebarios of sudden spikes due to unforsen events (i.e COVID-19, etc. ) 

## Solution
### Design Purpose

The journey to scale the current Syspos monolith is not a trivial one. There are many options and constraints to abide by. At core the architecture team is refactoring the existing design to achieve better qualities. For example, to improve user experience during ticket creation we are carving out the Ticket Creation component into an independent service so that more resources can be allocated to it and hence achieve better performance. The purpose of the design is to describe the current system (the monolith), propose a new system that solves the challenges with the current monolith and provide guides of the construction process

### Primary Functional Requirements
The core of the Sysops system is to route experts to failing equipment to help customers achieve better quality of life. UC-6, UC-7,UC-8 and UC-9 demonstrate the core functionality of the system. A system that can not accommodate these use cases is a failing system.     

### Ranking of the Quality Attribute Scenarios

Scenario ID | Importance to Customer| Difficulty of implementation according to architecture
------------| ----------------------|--------------------------------------------------------
QAS-1 | High | High
QAS-2 | Medium | Low
QAS-3 | High | Medium
QAS-4 | Medium | High
QAS-5 | Low | Low
QAS-6 | Low | Low
QAS-7 | Low | High


