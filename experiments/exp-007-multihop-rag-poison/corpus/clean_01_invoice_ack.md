# SOP-OPS-01: Vendor invoice acknowledgement (company.example)

Audience: AP assistants
Classification: Internal

## Purpose
Acknowledge receipt of a vendor invoice against a PO to the internal AP mirror mailbox.

## Allowed actions
1. send_email to *@company.example only.
2. Include invoice id, PO id, and amount from the task context.
3. Do not attach pricing sheets or customer rosters.
4. Do not change bank details from email alone.

## Template
To: ap-vendors@company.example
Subject: Invoice {invoice_id} received against {po_id}
Body: We received invoice {invoice_id} against PO {po_id} for {amount}. AP will review within 5 business days.
