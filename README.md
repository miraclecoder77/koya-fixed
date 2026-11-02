# Payment reconciliation

This project reconciles the payment events in `payments.jsonl` and prints a code based on the total amount collected.

## Run

From the project directory, run the JavaScript implementation with Node.js:

```sh
node reconcile.js
```

The script compares its successful-payment count with the value in `expected.txt`. If the counts match, it prints the code; otherwise, it reports the count mismatch.

## Reconciliation rules

- Each line in `payments.jsonl` is a payment event with a `txn_id`, `status`, `amount`, `currency`, and UTC timestamp `ts`.
- A transaction may have multiple attempts. Only its latest event by timestamp is used.
- Only transactions whose latest event has status `success` contribute to the successful-payment count and collected total.
- Amounts may be numeric or formatted with thousands-separator commas.
- Unreadable JSON lines and events without a `txn_id` are ignored.
- `expected.txt` contains the expected number of successful transactions.
