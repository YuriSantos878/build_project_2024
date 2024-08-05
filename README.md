# build_project_2024
CREATE TABLE Hospitals (
    hospital_id INT PRIMARY KEY,
    hospital_name VARCHAR(100),
    hospital_address VARCHAR(100),
    hospital_city VARCHAR(50),
    hospital_state VARCHAR(2),
    hospital_zip VARCHAR(10),
    hospital_phone VARCHAR(15)
);

CREATE TABLE HealthCareProviders (
    provider_id INT PRIMARY KEY,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    dob DATE,
    gender VARCHAR(1),
    npi VARCHAR(10),
    address VARCHAR(100),
    city VARCHAR(50),
    state VARCHAR(2),
    zip VARCHAR(10),
    phone VARCHAR(15),
    hospital_id INT,
    role VARCHAR(50),
    FOREIGN KEY (hospital_id) REFERENCES Hospitals(hospital_id)
);

CREATE TABLE Patients (
    patient_id INT PRIMARY KEY,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    dob DATE,
    gender VARCHAR(1),
    mrn VARCHAR(10),
    ssn VARCHAR(11),
    insurance_id VARCHAR(10),
    hospital_id INT,
    FOREIGN KEY (hospital_id) REFERENCES Hospitals(hospital_id)
);

CREATE TABLE MedicalClaims (
    claim_id INT PRIMARY KEY,
    patient_id INT,
    provider_id INT,
    ndc VARCHAR(12),
    quantity INT,
    total_amount DECIMAL(10, 2),
    days_supply INT,
    prescription_number VARCHAR(10),
    date_filled DATE,
    FOREIGN KEY (patient_id) REFERENCES Patients(patient_id),
    FOREIGN KEY (provider_id) REFERENCES HealthCareProviders(provider_id)
);

-- Insert into Hospitals
INSERT INTO Hospitals (hospital_id, hospital_name, hospital_address, hospital_city, hospital_state, hospital_zip, hospital_phone)
VALUES (1, 'General Hospital', '123 Main St', 'Springfield', 'IL', '62701', '217-555-1234'),
       (2, 'Mercy Medical Center', '456 Elm St', 'Hartford', 'CT', '06103', '860-555-5678'),
       (3, 'City Health Clinic', '789 Maple Ave', 'Columbus', 'OH', '43215', '614-555-7890');

-- Insert into HealthCareProviders
INSERT INTO HealthCareProviders (provider_id, first_name, last_name, dob, gender, npi, address, city, state, zip, phone, hospital_id, role)
VALUES (1, 'John', 'Smith', '1975-01-01', 'M', '1234567890', '100 Park Ave', 'Springfield', 'IL', '62701', '217-555-1111', 1, 'Doctor'),
       (2, 'Alice', 'Johnson', '1980-05-12', 'F', '2345678901', '200 Oak St', 'Hartford', 'CT', '06103', '860-555-2222', 2, 'Nurse'),
       (3, 'Robert', 'Brown', '1968-09-30', 'M' , '4327334087', '300 Riley Rd', 'New Windsor', 'NY', '12553', '810-631-0185', 3, 'Doctor');


