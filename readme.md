# CLT Assignment - Richard Soegito

## 📌 Overview

This project implements a hierarchical data structure:

**Supplier → Layups → Layers**

Each Supplier can have multiple Layups, and each Layup contains multiple Layers.

The application provides:

* Full CRUD functionality
* Import / Export system
* Conflict detection & resolution (including UI-based manual resolution)

---

## 🧱 Data Structure

Supplier
└── Layups
└── Layers

### Relationship:

* Supplier hasMany Layups
* Layup hasMany Layers

---

## ⚙️ Setup Instructions

### 1. Clone Repository

```bash
git clone https://github.com/richardsoegito/clt-assignment.git
cd clt-assignment
git checkout richard-assignment
```

### 2. Install Dependencies

```bash
composer install
npm install
```

### 3. Environment Setup

```bash
cp .env.example .env
php artisan key:generate
```

### 4. Database

```bash
php artisan migrate
```

### 5. Run Application

```bash
php artisan serve
```

---

## 🚀 Features

### ✅ CRUD Features

#### Supplier

* Create Supplier
* Edit Supplier
* Delete Supplier

#### Layups (Nested under Supplier)

* Create Layup
* Edit Layup
* Delete Layup

#### Layers (Nested under Layup)

* Create Layer
* Edit Layer
* Delete Layer

---

## 📤 Export Features

### Export by Supplier

Exports:

* Supplier
* All related Layups
* All related Layers

### Export by Layup

Exports:

* Layup
* All related Layers

### Export by Layer

Exports:

* Single Layer data

---

## 📥 Import Features

### Import by Supplier

* Accepts JSON input
* Automatically:

  * Creates new Layups
  * Creates new Layers
  * Updates existing Layers (depending on strategy)

---

## ⚠️ Conflict Detection Rules

### 1. Layup-Level

If:

* Layup name already exists under the same supplier

➡️ Treated as the same Layup (NOT duplicated)

---

### 2. Layer-Level

If:

* Same `layer_order` exists
* BUT values differ (`thickness`, `width`, `angle`)

➡️ This is considered a **CONFLICT**

---

## 🔥 Conflict Resolution Strategies

### 1. Overwrite

* Incoming data replaces existing data

### 2. Skip

* Existing data is preserved
* Incoming data ignored

### 3. Manual Resolve (UI-Based) ⭐

* Displays:

  * Existing Data vs Incoming Data
* Highlights differences (in red)
* User can choose:

  * ✅ Keep Existing
  * ✅ Accept Incoming
* Resolve conflicts one-by-one

---

## 🖥️ Conflict Resolution UI

Features:

* Side-by-side comparison
* Highlighted differences (red text)
* Action buttons:

  * Keep Existing
  * Accept Incoming
* Dynamic conflict count

---

## 🧪 Example Import JSON

### Normal Import

```json
{
  "layups": [
    {
      "name": "Layup Alpha",
      "layers": [
        {
          "layer_order": 1,
          "thickness": 50,
          "width": 100,
          "angle": 0
        }
      ]
    }
  ]
}
```

---

### Conflict Example

```json
{
  "layups": [
    {
      "name": "Layup Alpha",
      "layers": [
        {
          "layer_order": 1,
          "thickness": 999,
          "width": 999,
          "angle": 999
        }
      ]
    }
  ]
}
```

---

## 🎥 Demo Video

👉 https://drive.google.com/drive/folders/1nTeMMw6iaCim3EQ6WM73fZMhInO75HsW?usp=drive_link

---

## 🧠 Technical Approach

* Nested Resource Routing (Laravel)
* Eloquent Relationships
* Session-based Conflict Handling
* Dynamic UI Rendering for conflicts

---

## 🛠 Tech Stack

* Laravel
* MySQL
* Tailwind CSS

---

## 📌 Notes

* Designed to follow Laravel best practices
* Conflict resolution inspired by Git merge behavior
* Clean and modular controller logic
* Scalable structure for future improvements

---

## 🔍 Possible Improvements

* Repository Pattern implementation
* Service Layer abstraction
* Automated Testing (Unit & Feature)
* Upload file import (CSV / Excel)
* Pagination for large datasets

---

## 👨‍💻 Author

Richard Soegito
