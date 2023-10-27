### List all doctors' information
````sql
SELECT * FROM Doctors;
````

### List all information of patients whose last name is "Nguyen"
````sql
SELECT * FROM Patients WHERE last_name = "Nguyen";
````

### List all names of drugs which have their quantity in stock more than 200
````sql
SELECT drug_name FROM Drug WHERE stock_quantity > 200;
````

### List all information of transactions that have the dispensing fee greater than 5 dollars and have the drug id of 3
````sql
SELECT * FROM Transaction WHERE Dispensing_fee > 5 AND drug_id = 3;
````

### List all information of prescriptions that have the dosage level higher than 5
````sql
SELECT * FROM Prescriptions WHERE DOSAGE > 5;
````

### List the employee information that has the last 3 digits of their phone number as 460
````sql
SELECT employee_id, first_name, last_name FROM Employee WHERE phone_number LIKE '%460%';
````

### List the phone number of Moderna company
````sql
SELECT company_name, phone_number FROM Drug_company WHERE company_name = "Moderna";
````

### List all transaction information which has the quantity of drug larger than 2
````sql
SELECT * FROM Transaction WHERE Quantity > 2;
````

## Advanced queries
### List the information of doctors that prescribe the most
````sql
SELECT d.doctor_id, d.first_name, d.last_name, MAX(no_prescription)
FROM doctors d
INNER JOIN (
    SELECT doctor_id, COUNT(*) AS no_prescription
    FROM Prescriptions
    GROUP BY doctor_id
) p
ON d.doctor_id = p.doctor_id;
````

### List the drug id that has no sale yet
````sql
SELECT d.drug_id
FROM drug d
LEFT JOIN Transaction t
ON d.drug_id = t.drug_id
WHERE t.drug_id IS NULL;
````

### Select the company that sells the most drugs
````sql
SELECT dp.company_id, dp.company_name
FROM drug_company dp
INNER JOIN (
    SELECT company_id, COUNT(company_id) AS no_drug
    FROM drug
    GROUP BY company_id
) d
ON dp.company_id = d.company_id
ORDER BY no_drug
LIMIT 1;
````

### List total revenue of that pharmacy
````sql
SELECT SUM(t.quantity * d.drug_price + t.Dispensing_fee) AS total_revenue
FROM transaction t
JOIN drug d ON t.drug_id = d.drug_id;
````

### List top 3 patients who pay the most money
````sql
SELECT t.patient_id, p.first_name, p.last_name, SUM(t.quantity * d.drug_price + t.Dispensing_fee) AS total_amount
FROM transaction t
JOIN drug d ON t.drug_id = d.drug_id
JOIN patients p ON t.patient_id = p.patient_id
GROUP BY t.patient_id
ORDER BY total_amount DESC
LIMIT 3;
````

### List the quantity of the drug that was sold
````sql
SELECT d.drug_name, t.no_drug FROM drug d
JOIN (
    SELECT drug_id, COUNT(drug_id) AS no_drug
    FROM transaction
    GROUP BY drug_id
) t
ON d.drug_id = t.drug_id;
````

## Update commands
### Update doctor's phone number that has id 1
````sql
UPDATE doctors
SET phone_number = "451-450-200"
WHERE doctor_id = 1;
````

### Update stock's quantity of drug that has ID number 2
````sql
UPDATE drug
SET stock_quantity = 40
WHERE drug_id = 2;
````

### Update dosage of prescription ID 4
````sql
UPDATE Prescriptions
SET dosage = 2
WHERE prescription_id = 4;
````

### Update dispensing fee for patient that has patient ID 1
````sql
UPDATE transaction
SET Dispensing_fee = 3
WHERE patient_id = 1;
````

## Delete commands
### Delete drug information that is out of stock
````sql
DELETE FROM drug
WHERE drug_id = 2;
````

### Delete patient information that has patient ID 1
````sql
DELETE FROM Patients
WHERE patient_id = 1;
````

### Delete transaction that has transaction ID 4
````sql
DELETE FROM transaction
WHERE Trans_id = 4;
````

### Delete drug company that has company ID 3
````sql
DELETE FROM drug_company
WHERE company_id = 3;
````
