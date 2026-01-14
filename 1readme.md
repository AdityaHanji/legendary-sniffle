# MSME Invoice Dashboard

A high-performance React application designed for MSMEs to track invoices, manage cash flow, and monitor payment delays.

🚀 **Live Demo:** [Insert Netlify/Vercel Link]

---

## 🏗 Approach

### Component Structure
I adopted a **modular component-based architecture** to ensure separation of concerns and scalability:
* **Context API (`InvoiceContext`)**: Serves as the "Single Source of Truth." It handles the core business logic, status auto-calculations, and bulk data operations globally to avoid prop-drilling.
* **Smart Containers (`App.jsx`)**: Manages the orchestration of search, multi-status filtering, and pagination.
* **Utility Layer (`utils/analytics.js`)**: Encapsulates complex temporal logic and financial calculations, keeping the UI components "lean" and focused only on rendering.

### Challenges Faced
* **Handling Large Datasets**: To prevent the browser from freezing when generating 500+ invoices, I implemented a **Batch Update Strategy**. Instead of 500 individual state updates, data is constructed in memory and injected into the state in a single cycle.
* **Temporal Accuracy**: Calculating "Days Overdue" vs "Paid Early/Late" across timezones can be buggy. I solved this by using **Normalized Temporal Logic**, stripping time data to compare strict `YYYY-MM-DD` strings.

---

## ⚡ Performance Optimizations

### 1. Virtual Batch Injection
Standard iterative updates can crash a React app during stress tests. My implementation uses a specialized `addBulkInvoices` function that batches hundreds of records into one update, ensuring the UI remains fluid even with massive datasets.

### 2. Memoized Data Processing (`useMemo`)
All expensive operations—including the multi-criteria filtering, sorting, and the 4 summary card calculations—are wrapped in `useMemo`. This ensures that a user typing in the search bar doesn't trigger a full recalculation of the entire dataset's analytics.

### 3. Self-Hydrating Persistence
I implemented a persistence layer that automatically bridges `localStorage` with the React state. The application "hydrates" itself on initial load and uses a `useEffect` observer to silently sync every change, meeting the requirement for data persistence across refreshes.



---

## ⏱ Time Breakdown

| Task | Hours |
| :--- | :--- |
| **Design & Planning** | 1.5 Hours |
| **Development** | 9.0 Hours |
| **Testing, Optimization & Debugging** | 3.5 Hours |
| **Total Time** | **14 Hours** |

---

## 🛠 Setup & Run

1. **Clone the repo:** `git clone [Your-Repo-URL]`
2. **Install dependencies:** `npm install`
3. **Start local server:** `npm run dev`
