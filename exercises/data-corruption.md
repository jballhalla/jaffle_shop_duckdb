Error: "excelsior" inserted into `customers` model source table, at ./seeds/raw_orders col `status` row 9



uv run dbt build --select +customers
...
17:34:26  10 of 18 FAIL 1 accepted_values_stg_orders_status__placed__shipped__completed__return_pending__returned  [FAIL 1 in 0.09s]
...
17:34:26  [ERROR]: in test accepted_values_stg_orders_status__placed__shipped__completed__return_pending__returned (models/staging/schema.yml)
17:34:26    Got 1 result, configured to fail if != 0
17:34:26  
17:34:26    compiled code at target/compiled/jaffle_shop/models/staging/schema.yml/accepted_values_stg_orders_4f514bf94b77b7ea437830eec4421c58.sql
17:34:26  
17:34:26  Done. PASS=13 WARN=0 ERROR=1 SKIP=4 NO-OP=0 REUSED=0 TOTAL=18


//

id=$(jq -r '
  .results[]
  | select(.unique_id | contains("accepted_values_stg_orders_status"))
  | .unique_id
' target/run_results.json)

jq --arg id "$id" '
  .nodes[$id]
  | {name, original_file_path, column_name, test_metadata}
' target/manifest.json
...
{
  "name": "accepted_values_stg_orders_status__placed__shipped__completed__return_pending__returned",
  "original_file_path": "models/staging/schema.yml",
  "column_name": "status",
  "test_metadata": {
    "name": "accepted_values",
    "kwargs": {
      "column_name": "status",
      "values": [
        "placed",
        "shipped",
        "completed",
        "return_pending",
        "returned"
      ],
      "model": "{{ get_where_subquery(ref('stg_orders')) }}"
    },
    "namespace": null
  }
}

//

git restore seeds/raw_orders.csv

//

uv run dbt test
17:42:59  Running with dbt=1.12.5
17:42:59  Registered adapter: duckdb=1.11.0
17:42:59  Found 5 models, 3 seeds, 20 data tests, 500 macros
17:42:59  
17:42:59  Concurrency: 24 threads (target='dev')
17:42:59  
17:42:59  1 of 20 START test accepted_values_orders_status__placed__shipped__completed__return_pending__returned  [RUN]
17:42:59  2 of 20 START test accepted_values_stg_orders_status__placed__shipped__completed__return_pending__returned  [RUN]
17:42:59  7 of 20 START test not_null_orders_coupon_amount ............................... [RUN]
17:42:59  10 of 20 START test not_null_orders_gift_card_amount ........................... [RUN]
17:42:59  4 of 20 START test not_null_customers_customer_id .............................. [RUN]
17:42:59  13 of 20 START test not_null_stg_orders_order_id ............................... [RUN]
17:42:59  6 of 20 START test not_null_orders_bank_transfer_amount ........................ [RUN]
17:42:59  15 of 20 START test relationships_orders_customer_id__customer_id__ref_customers_  [RUN]
17:42:59  11 of 20 START test not_null_orders_order_id ................................... [RUN]
17:42:59  12 of 20 START test not_null_stg_customers_customer_id ......................... [RUN]
17:42:59  16 of 20 START test unique_customers_customer_id ............................... [RUN]
17:42:59  18 of 20 START test unique_stg_customers_customer_id ........................... [RUN]
17:42:59  17 of 20 START test unique_orders_order_id ..................................... [RUN]
17:42:59  5 of 20 START test not_null_orders_amount ...................................... [RUN]
17:42:59  3 of 20 START test accepted_values_stg_payments_payment_method__credit_card__coupon__bank_transfer__gift_card  [RUN]
17:42:59  9 of 20 START test not_null_orders_customer_id ................................. [RUN]
17:42:59  14 of 20 START test not_null_stg_payments_payment_id ........................... [RUN]
17:42:59  19 of 20 START test unique_stg_orders_order_id ................................. [RUN]
17:42:59  20 of 20 START test unique_stg_payments_payment_id ............................. [RUN]
17:42:59  8 of 20 START test not_null_orders_credit_card_amount .......................... [RUN]
17:42:59  11 of 20 PASS not_null_orders_order_id ......................................... [PASS in 0.19s]
17:42:59  4 of 20 PASS not_null_customers_customer_id .................................... [PASS in 0.19s]
17:42:59  13 of 20 PASS not_null_stg_orders_order_id ..................................... [PASS in 0.19s]
17:42:59  6 of 20 PASS not_null_orders_bank_transfer_amount .............................. [PASS in 0.19s]
17:42:59  12 of 20 PASS not_null_stg_customers_customer_id ............................... [PASS in 0.19s]
17:42:59  10 of 20 PASS not_null_orders_gift_card_amount ................................. [PASS in 0.19s]
17:42:59  7 of 20 PASS not_null_orders_coupon_amount ..................................... [PASS in 0.19s]
17:42:59  5 of 20 PASS not_null_orders_amount ............................................ [PASS in 0.19s]
17:42:59  9 of 20 PASS not_null_orders_customer_id ....................................... [PASS in 0.19s]
17:42:59  2 of 20 PASS accepted_values_stg_orders_status__placed__shipped__completed__return_pending__returned  [PASS in 0.19s]
17:42:59  3 of 20 PASS accepted_values_stg_payments_payment_method__credit_card__coupon__bank_transfer__gift_card  [PASS in 0.19s]
17:42:59  1 of 20 PASS accepted_values_orders_status__placed__shipped__completed__return_pending__returned  [PASS in 0.19s]
17:42:59  14 of 20 PASS not_null_stg_payments_payment_id ................................. [PASS in 0.19s]
17:42:59  8 of 20 PASS not_null_orders_credit_card_amount ................................ [PASS in 0.19s]
17:42:59  20 of 20 PASS unique_stg_payments_payment_id ................................... [PASS in 0.19s]
17:42:59  15 of 20 PASS relationships_orders_customer_id__customer_id__ref_customers_ .... [PASS in 0.19s]
17:42:59  17 of 20 PASS unique_orders_order_id ........................................... [PASS in 0.19s]
17:42:59  16 of 20 PASS unique_customers_customer_id ..................................... [PASS in 0.19s]
17:42:59  19 of 20 PASS unique_stg_orders_order_id ....................................... [PASS in 0.19s]
17:42:59  18 of 20 PASS unique_stg_customers_customer_id ................................. [PASS in 0.19s]
17:42:59  
17:42:59  Finished running 20 data tests in 0 hours 0 minutes and 0.27 seconds (0.27s).
17:42:59  
17:42:59  Completed successfully
17:42:59  
17:42:59  Done. PASS=20 WARN=0 ERROR=0 SKIP=0 NO-OP=0 REUSED=0 TOTAL=20

