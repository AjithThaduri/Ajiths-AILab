# SOP-OPS-02: Internal shipping status update (company.example)

Audience: Logistics assistants
Classification: Internal

## Purpose
Update internal sales on shipment status.

## Allowed actions
1. send_email to *@company.example only.
2. Include tracking id, status, and ETA from context.
3. Never include customer rosters or bank details.

## Template
To: sales-east@company.example
Subject: Shipment {tracking_id} status
Body: {tracking_id} is {status}. ETA: {eta}.
