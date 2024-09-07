# Medical Insurance Database Schema - README

## Overview

This document provides an overview of the database schema designed to manage data related to members, claims, insurance products, and healthcare providers within a medical insurance system. The schema is structured to capture essential information about insured members, the insurance products they are enrolled in, claims filed by members, and details about the healthcare providers involved.

## Tables and Relationships

### 1. **Members Table**
The Members table stores personal and insurance-related details about individuals who are insured.

- **Table Name**: `members`
- **Primary Key**: `member_id`

| Column Name    | Data Type     | Description                                  |
|----------------|---------------|----------------------------------------------|
| `member_id`    | `INT`         | Primary Key. Unique ID for each member.      |
| `first_name`   | `VARCHAR(50)` | Member's first name.                         |
| `last_name`    | `VARCHAR(50)` | Member's last name.                          |
| `dob`          | `DATE`        | Date of birth.                               |
| `gender`       | `VARCHAR(10)` | Gender of the member.                        |
| `address`      | `VARCHAR(255)`| Member's address.                            |
| `phone_number` | `VARCHAR(15)` | Contact number.                              |
| `email`        | `VARCHAR(100)`| Email address.                               |
| `start_date`   | `DATE`        | Date when the member's insurance started.    |
| `end_date`     | `DATE`        | Date when the member's insurance ended (if applicable). |
| `product_id`   | `INT`         | Foreign Key. References `insurance_product.product_id`. |

### 2. **Insurance Products Table**
The Insurance Products table defines the various insurance products available to members.

- **Table Name**: `insurance_products`
- **Primary Key**: `product_id`

| Column Name      | Data Type     | Description                                  |
|------------------|---------------|----------------------------------------------|
| `product_id`     | `INT`         | Primary Key. Unique ID for each product.     |
| `product_name`   | `VARCHAR(100)`| Name of the insurance product.               |
| `coverage_type`  | `VARCHAR(50)` | Type of coverage (e.g., HMO, PPO, etc.).     |
| `premium_amount` | `DECIMAL(10,2)`| Monthly premium amount.                      |
| `deductible`     | `DECIMAL(10,2)`| Deductible amount.                           |
| `out_of_pocket_max` | `DECIMAL(10,2)`| Maximum out-of-pocket expense.             |
| `network_type`   | `VARCHAR(50)` | Network type (e.g., in-network, out-of-network). |

### 3. **Claims Table**
The Claims table stores the details of each claim made by members, including the amount claimed, amount paid, and the status of the claim.

- **Table Name**: `claims`
- **Primary Key**: `claim_id`

| Column Name       | Data Type     | Description                                  |
|-------------------|---------------|----------------------------------------------|
| `claim_id`        | `INT`         | Primary Key. Unique ID for each claim.       |
| `member_id`       | `INT`         | Foreign Key. References `members.member_id`. |
| `provider_id`     | `INT`         | Foreign Key. References `providers.provider_id`. |
| `date_of_service` | `DATE`        | Date when the service was provided.          |
| `date_of_claim`   | `DATE`        | Date when the claim was filed.               |
| `claim_amount`    | `DECIMAL(10,2)`| Total amount of the claim.                   |
| `paid_amount`     | `DECIMAL(10,2)`| Amount paid by the insurance.                |
| `claim_status`    | `VARCHAR(20)` | Status of the claim (e.g., approved, denied, pending). |
| `diagnosis_code`  | `VARCHAR(10)` | ICD code for the diagnosis.                  |
| `procedure_code`  | `VARCHAR(10)` | CPT code for the procedure performed.        |

### 4. **Providers Table**
The Providers table captures information about healthcare providers who offer services to insured members.

- **Table Name**: `providers`
- **Primary Key**: `provider_id`

| Column Name      | Data Type     | Description                                  |
|------------------|---------------|----------------------------------------------|
| `provider_id`    | `INT`         | Primary Key. Unique ID for each provider.    |
| `provider_name`  | `VARCHAR(100)`| Name of the healthcare provider.             |
| `specialty`      | `VARCHAR(50)` | Provider's specialty.                        |
| `phone_number`   | `VARCHAR(15)` | Contact number.                              |
| `address`        | `VARCHAR(255)`| Address of the provider.                     |
| `network_status` | `VARCHAR(20)` | In-network or out-of-network.                |

### 5. **Claim Details Table** (Optional)
The Claim Details table provides a detailed itemization of services within a claim, including specific services provided, their costs, and the dates they were performed.

- **Table Name**: `claim_details`
- **Primary Key**: `claim_detail_id`

| Column Name      | Data Type     | Description                                  |
|------------------|---------------|----------------------------------------------|
| `claim_detail_id`| `INT`         | Primary Key. Unique ID for each detail entry.|
| `claim_id`       | `INT`         | Foreign Key. References `claims.claim_id`.   |
| `service_code`   | `VARCHAR(10)` | Code for the specific service provided.      |
| `service_description` | `VARCHAR(255)`| Description of the service provided.   |
| `service_amount` | `DECIMAL(10,2)`| Amount for the specific service.             |
| `service_date`   | `DATE`        | Date when the service was provided.          |

## Relationships

- **Members ↔ Insurance Products**: Each member is enrolled in an insurance product (`members.product_id` references `insurance_products.product_id`).
- **Claims ↔ Members**: Each claim is associated with a member (`claims.member_id` references `members.member_id`).
- **Claims ↔ Providers**: Each claim is associated with a provider (`claims.provider_id` references `providers.provider_id`).
- **Claim Details ↔ Claims**: Detailed services within a claim are linked to a specific claim (`claim_details.claim_id` references `claims.claim_id`).

## Usage Notes

- This schema is designed for scalability and can be extended with additional tables and relationships as needed.
- Care should be taken to maintain referential integrity between the tables to ensure data consistency.
- The optional Claim Details table is useful for itemizing and analyzing the specific services rendered within each claim.

## Versioning

This document outlines version 1.0 of the medical insurance database schema. Future updates may include additional fields, tables, and relationships to support expanded functionality.
