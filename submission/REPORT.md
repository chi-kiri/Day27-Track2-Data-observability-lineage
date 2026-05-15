# Lab Report: Sales Data Quality Pipeline & Observability

**Student Name:** [Your Name]  
**Date:** 2026-05-15  
**Course:** AI Thực Chiến - Day 27  

---

## 1. Objective
The goal of this lab was to implement a data quality observability pipeline using Apache Airflow. The pipeline validates incoming sales order data (CSV), generates a validation summary (JSON), and sends automated notifications to a Discord channel via Webhooks.

## 2. Implementation Details

### 2.1 Validation Rules
- **Customer ID**: Must be present (non-empty).
- **Amount**: Must be a positive numeric value (> 0).
- **Status**: Must be one of the pre-defined valid statuses: `completed`, `pending`, `cancelled`.

### 2.2 Core Logic
- Developed `src/validation.py` to handle CSV parsing and rule checking.
- Configured `src/config.py` with environment variable support (via `.env`) for the Discord Webhook URL.
- Implemented the `validate_orders_task` in the Airflow DAG to orchestrate the validation process.

## 3. Results & Verification

### 3.1 Local Execution Results
The system was verified locally using the `run_local_check.py` utility against two datasets:
- **`orders_passed.csv`**: All 10 rows passed validation.
- **`orders_failed.csv`**: Correctly identified 2 missing customer IDs, 2 invalid amounts, and 2 invalid statuses.

### 3.2 Discord Notifications
Automated alerts were successfully delivered to the Discord channel for both success and failure scenarios, providing real-time observability into the data pipeline's health.

---

## 4. Evidence (Screenshots)

### 4.1 Validation Summary (JSON)
The following summary was generated after the failed dataset run:
```json
{
  "row_count": 10,
  "missing_customer_ids": 2,
  "invalid_amounts": 2,
  "invalid_statuses": 2,
  "validation_status": "failed"
}
```

### 4.2 Terminal Execution & Discord Alerts
Refer to the screenshots in the `submission/` folder:
- `01_passed_dataset_test.png`
- `02_failed_dataset_test.png`
- `03_discord_notification.png`

---

## 5. Conclusion
The pipeline successfully implements basic data observability and lineage principles by ensuring that only high-quality data proceeds through the system, while providing immediate feedback to stakeholders via Discord notifications.
