# Welcome to the MindsDB Manual QA Testing for MySQL Plaid Handler


## Testing MySQL Handler with [Transactions](URL to the Dataset)

**1. Testing CREATE DATABASE**

```
CREATE DATABASE my_plaid 
WITH 
    ENGINE = 'plaid',
    PARAMETERS = {
      "client_id": "YOUR_CLIENT_ID",
      "secret": "YOUR_SECRET",
      "access_token": "YOUR_PUBLIC_KEY",
      "plaid_env": "ENV"
    };
``` 

![CREATE_DATABASE]('/c/Users/Mohammed Shakeel/Documents/shakeel/Screenshot (67).png')

**2. Testing CREATE PREDICTOR**

```
CREATE MODEL mindsdb.expense_prediction
FROM my_plaid 
    ( SELECT  merchant_name, date, amount 
      FROM transactions 
      WHERE start_date='2023-01-01' 
      AND end_date='2023-04-11' )
PREDICT amount
ORDER BY date
GROUP BY merchant_name
WINDOW 25
HORIZON 15
USING ENGINE = 'statsforecast';
```

![CREATE_PREDICTOR]('/c/Users/Mohammed Shakeel/Documents/shakeel/Screenshot (66).png')

**3. Testing SELECT FROM PREDICTOR**

```
SELECT * FROM mindsdb.models
WHERE name='expense_prediction'
```

![SELECT_FROM]('/c/Users/Mohammed Shakeel/Documents/shakeel/Screenshot (77).png')

### Results

Drop a remark based on your observation.
- [ ] Works Great 💚 (This means that all the steps were executed successfully and the expected outputs were returned.)
- [*] There's a Bug 🪲 [Unable to Create Model with Plaid Data Source: Syntax Error(https://github.com/mindsdb/mindsdb/issues/8171)

---
