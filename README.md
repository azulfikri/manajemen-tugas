# Sistem Rental Mobil

```mermaid
erDiagram
    USERS ||--o{ RENTALS : makes
    USERS ||--o{ REVIEWS : writes

    CARS ||--o{ RENTALS : is_rented_in
    CARS ||--o{ REVIEWS : receives

    CATEGORIES ||--o{ CARS : includes
    BRANDS ||--o{ CARS : manufactures

    RENTALS ||--o{ PAYMENTS : has
    RENTALS ||--o{ REVIEWS : triggers

    USERS {
        int id PK
        string name
        string email UNIQUE
        string password
        string phone UNIQUE, nullable
        enum role "admin,customer"
        string ktp_number nullable
        string driver_license_number nullable
        datetime created_at
        datetime updated_at
    }

    CATEGORIES {
        int id PK
        string name UNIQUE
        text description nullable
        datetime created_at
        datetime updated_at
    }

    BRANDS {
        int id PK
        string name UNIQUE
        datetime created_at
        datetime updated_at
    }

    CARS {
        int id PK
        int category_id FK
        int brand_id FK
        string model
        string license_plate UNIQUE
        int year
        decimal price_per_day
        text description nullable
        enum status "available,unavailable,maintenance"
        string image nullable
        datetime created_at
        datetime updated_at
    }

    RENTALS {
        int id PK
        int user_id FK
        int car_id FK
        datetime start_date
        datetime end_date
        decimal total_price
        enum status "pending,confirmed,ongoing,completed,canceled"
        string pickup_location nullable
        datetime created_at
        datetime updated_at
    }

    PAYMENTS {
        int id PK
        int rental_id FK
        enum method "bank_transfer,credit_card,ewallet"
        decimal amount
        enum status "pending,paid,failed"
        datetime paid_at nullable
        string transaction_id nullable
        datetime created_at
        datetime updated_at
    }

    REVIEWS {
        int id PK
        int user_id FK
        int car_id FK
        int rental_id FK, nullable
        int rating
        text comment nullable
        datetime created_at
        datetime updated_at
    }


```
