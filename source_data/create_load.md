# Schema Design

## Table: Doctors
````sql

CREATE TABLE Doctors (
        doctor_id INT PRIMARY KEY,
        first_name VARCHAR(50) NOT NULL,
        last_name VARCHAR(50) NOT NULL,
        specialty VARCHAR(50) NOT NULL,
        phone_number VARCHAR(15)
);
````

## Table: Patients
````sql
CREATE TABLE Patients (
        patient_id INT PRIMARY KEY,
        first_name VARCHAR(50) NOT NULL,
        last_name VARCHAR(50) NOT NULL,
        birthdate DATE NOT NULL,
        gender CHAR(1) NOT NULL,
        phone_number VARCHAR(15),
        insurance_no INT NOT NULL
);
````

## Table: Drug
````sql
CREATE TABLE Drug (
        drug_id INT PRIMARY KEY,
        drug_name VARCHAR(50) NOT NULL,
        stock_quantity INT NOT NULL,
        drug_strength INT NOT NULL,
        pack_size INT NOT NULL,
        drug_price INT NOT NULL,
        company_id INT NOT NULL,
        CONSTRAINT fk_drug_company
                FOREIGN KEY (company_id)
                REFERENCES Drug_company(company_id)
);
````

## Table: Transaction
````sql
CREATE TABLE Transaction (
     Trans_id INT PRIMARY KEY,
     Trans_date DATE NOT NULL,
        Dispensing_fee INT NOT NULL,
     Quantity INT NOT NULL,
        drug_id INT NOT NULL,
        patient_id INT NOT NULL,
     CONSTRAINT fk_drug
                FOREIGN KEY (drug_id)
                REFERENCES drug(drug_id),
        CONSTRAINT fk_patient_id
                FOREIGN KEY (patient_id)
                REFERENCES Patients(patient_id)
);
````

## Table: Prescriptions
````sql
CREATE TABLE Prescriptions (
        prescription_id INT PRIMARY KEY,
        patient_id INT NOT NULL,
        doctor_id INT NOT NULL,
        drug_id INT NOT NULL,
        prescription_date DATE NOT NULL,
        dosage INT NOT NULL,
        CONSTRAINT fk_drug_id
                FOREIGN KEY (drug_id)
                REFERENCES Drug(drug_id),
        CONSTRAINT fk_patient_id
                FOREIGN KEY (patient_id)
                REFERENCES Patients(patient_id),
        CONSTRAINT fk_doctor_id
                FOREIGN KEY (doctor_id)
                REFERENCES doctors(doctor_id)
);
````

## Table: Employee
````sql
CREATE TABLE Employee (
        employee_id INT PRIMARY KEY,
        first_name VARCHAR(50) NOT NULL,
        last_name VARCHAR(50) NOT NULL,
        phone_number VARCHAR(15)
);
````

## Table: Drug_company
````sql
CREATE TABLE Drug_company (
        company_id INT PRIMARY KEY,
        company_name VARCHAR(50) NOT NULL,
        phone_number VARCHAR(15)
);
````

## Database Construction: Populate Database
````sql
INSERT INTO Doctors (doctor_id, first_name, last_name, specialty, phone_number)
VALUES
    (1, 'Ha', 'Nguyen', 'Cardiology', '694-569-963'),
    (2, 'Anna', 'Le', 'Pediatrics', '603-950-325'),
    (3, 'Khang', 'Ly', 'Oncology', '515-227-579'),
    (4, 'Tho', 'Trong', 'Cardiology', '440-503-738 '),
    (5, 'Toan', 'Bui', 'Dermatology', '345-402-751');

INSERT INTO Patients (patient_id, first_name, last_name, birthdate, gender, phone_number, insurance_no)
VALUES
    (1, 'Trong', 'Vo', '2000-03-12', 'M', '056-307-698', 465996008),
    (2, 'Anh', 'Nguyen', '1967-08-10', 'F', '297-721-452', 905641067),
    (3, 'Van', 'Nguyen', '1999-10-30', 'M', '817-377-198', 698076154),
    (4, 'Trang', 'Trinh', '2001-07-19', 'M', '155-114-757', 897204172),
    (5, 'Hanh', 'Tran', '2000-10-20', 'M', '136-711-156', 111350358);

INSERT INTO Drug (drug_id, drug_name, stock_quantity, drug_strength, pack_size, drug_price, company_id)
VALUES
    (1, 'Acetaminophen', 200, 6, 20, 12.99, 2),
    (2, 'Alprazolam', 400, 8, 40, 19.99, 3),
    (3, 'Omeprazole', 200, 9, 80, 16.99, 1),
    (4, 'Cetirizine ', 300, 11, 10, 26.99, 2),
    (5, 'Metformin', 450, 12, 20, 28.99, 5)
;

INSERT INTO Transaction (Trans_id, Trans_date,Quantity, Dispensing_fee, drug_id, patient_id)
VALUES
    (1, '2022-02-21', 6, 8.99, 2, 2),
    (2, '2022-02-22', 2, 6.00, 4, 1),
    (3, '2022-02-23', 3, 7.99, 1, 1),
    (4, '2022-02-24', 1, 4.00, 3, 1),
    (5, '2022-02-25', 4, 6.99, 3, 4);

INSERT INTO Prescriptions (prescription_id, patient_id, doctor_id, drug_id, prescription_date, dosage)
VALUES
(1, 2, 4, 3, '2022-02-28', 2),
(2, 2, 4, 5, '2022-02-10', 7),
(3, 1, 2, 4, '2022-01-08', 10),
(4, 3, 1, 2, '2021-12-12', 1),
(5, 4, 3, 1, '2021-12-30', 8)
;
INSERT INTO Employee (employee_id, first_name, last_name, phone_number)
VALUES
    (1, 'An', 'Le', '475-376-358'),
    (2, 'Thanh', 'Trong', '058-379-845'),
    (3, 'Han', 'Nguyen', '652-853-674'),
    (4, 'Thu', 'Ha', '986-699-997'),
    (5, 'Tra', 'Thu', '325-373-460');

INSERT INTO Drug_company (company_id, company_name, phone_number)
VALUES
    (1, 'Pfizer', '141-907-846'),
    (2, 'Moderna', '872-608-429'),
    (3, 'Johnson & Johnson', '332-464-782'),
    (4, 'Sanofi', '926-713-204'),
    (5, 'Novartis', '152-332-993 ')
````