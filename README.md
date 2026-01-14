# MSME Invoice Dashboard

A robust, responsive React application designed to help **MSME (Micro, Small & Medium Enterprises)** business owners track invoices, manage cash flow, and monitor payments efficiently.

🚀 **Live Demo:** [aditya-hanji-msme-invoice-dashboard.netlify.app](https://aditya-hanji-msme-invoice-dashboard.netlify.app/)

---

## ✨ Key Features

* **📊 Smart Analytics:** Real-time calculation of Total Outstanding, Overdue amounts, Monthly Collections, and Average Payment Delay.
* **⚡ Bulk Data Generator:** A stress-testing tool capable of generating **500+ realistic invoices** instantly to test performance and pagination.
* **📄 Dynamic Pagination:** Efficiently browse large datasets with customizable rows per page (5, 10, 20, 50, 100).
* **🖨️ PDF Generation:** Client-side generation of professional invoice PDFs ready for download.
* **🌙 Dark Mode:** Fully responsive UI with a seamless dark/light theme toggle.
* **🛡️ Form Validation:** Strict validation ensuring no negative amounts or missing critical data.

---

## 🛠 Setup & Run

Follow these steps to run the project locally:

### 1. Installation
```bash
# Clone the repository
git clone [https://github.com/aditya-h-09/msme-invoice-dashboard.git](https://github.com/aditya-h-09/msme-invoice-dashboard.git)

# Navigate to project folder
cd msme-invoice-dashboard

# Install dependencies
npm install

# Start the development server
npm run dev

## 🏗 Approach

### Component Structure

I adopted a **modular component-based architecture** to ensure maintainability and scalability:

* **Context API (`InvoiceContext`)**: Acts as the "single source of truth" for application state. It handles CRUD operations, bulk data insertion, and complex business logic globally.
* **Presentational Components (`InvoiceTable`, `SummaryCards`)**: Pure components that receive data via props, making them highly reusable and easy to test.
* **Smart Containers (`App.jsx`)**: Handles the wiring of logic, state filtering, pagination, and layout composition.
* **Utility Layer (`utils/analytics.js`)**: Separates complex mathematical logic (date calculations, currency formatting) from UI code to keep components clean.

---

## 🧠 Challenges Faced

* **Handling Large Datasets (Performance)**: When implementing the "Generate 500 Invoices" feature, the app initially froze because I was updating the state 500 times in a loop.
    * **Solution**: I implemented a **Batch Update Strategy** (`addBulkInvoices`) to construct the data array in memory first and update the React state only once.
* **Accurate Analytics Logic**: Initially, the "Average Delay" and "Collected" cards showed "0" because the app wasn't tracking *when* a payment occurred.
    * **Solution**: I updated the data model to include a specific `paymentDate` field that is automatically set when an invoice is marked as "Paid".
* **Date Handling**: Managing timezones and calculating "days remaining" accurately was challenging.
    * **Solution**: I solved this by normalizing all dates to midnight strings (`YYYY-MM-DD`) before comparison.

---

## ⚡ Performance Optimizations

### 1. Batch State Processing
* **Where**: In `App.jsx` and `InvoiceContext.jsx`.
* **Why**: To support the bulk generation of data, iterative state updates were replaced with bulk operations. This prevents the React Reconciler from being overwhelmed, keeping the UI responsive even when adding hundreds of records at once.

### 2. Memoization (`useMemo`)
* **Where**: In `App.jsx` for search/filter/pagination logic and `SummaryCards.jsx` for total calculations.
* **Why**: Calculating totals and filtering large lists on every render is computationally expensive. `useMemo` ensures these calculations only re-run when the `invoices` array actually changes, preventing lag during search input.

### 3. Efficient DOM Updates
* **Where**: Status updates.
* **Why**: The app recalculates status (Overdue vs Pending) dynamically on the client side using the `calculateStatus` utility function. This keeps the UI reactive and in sync without unnecessary overhead.

### 4. Tailwind CSS (JIT)
* **Where**: Styling throughout the application.
* **Why**: Using Tailwind's Just-In-Time compiler allows for zero runtime style generation overhead compared to CSS-in-JS libraries, resulting in significantly faster initial page loads.

---

## ⏱ Time Breakdown

| Task | Hours |
| :--- | :--- |
| **Design & Planning** | 1.5 Hours |
| **Development** | 9.0 Hours |
| **Testing, Optimization & Debugging** | 3.5 Hours |
| **Total Time** | **14 Hours** |
