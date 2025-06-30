# clinic-booking-system
This is a Clinic Booking System Database with the following entities
- Patients
- Doctors
- Appointments
- Specializations
- Doctor_Specializations (M:N)
- Prescriptions



-- Patients Table
CREATE TABLE Patients (
    patient_id INT PRIMARY ,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    date_of_birth DATE,
    phone VARCHAR(20) UNIQUE,
    email VARCHAR(100) UNIQUE
);

-- Doctors Table
CREATE TABLE Doctors (
    doctor_id INT PRIMARY KEY,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    phone VARCHAR(20) UNIQUE,
    email VARCHAR(100) UNIQUE
);



-- Specializations Table
CREATE TABLE Specializations (
    specialization_id INT PRIMARY KEY ,
    name VARCHAR(100) UNIQUE NOT NULL
);

-- Junction Table for Doctor-Specialization (M:N)
CREATE TABLE Doctor_Specializations (
    doctor_id INT,
    specialization_id INT,
    PRIMARY KEY (doctor_id, specialization_id),
    FOREIGN KEY (doctor_id) REFERENCES Doctors(doctor_id),
    FOREIGN KEY (specialization_id) REFERENCES Specializations(specialization_id)
);

-- Appointments Table
CREATE TABLE Appointments (
    appointment_id INT PRIMARY KEY,
    patient_id INT NOT NULL,
    doctor_id INT NOT NULL,
    appointment_date DATETIME NOT NULL,
    reason TEXT,
    FOREIGN KEY (patient_id) REFERENCES Patients(patient_id),
    FOREIGN KEY (doctor_id) REFERENCES Doctors(doctor_id)
);

-- Prescriptions Table
CREATE TABLE Prescriptions (
    prescription_id INT PRIMARY KEY,
    appointment_id INT NOT NULL,
    medication VARCHAR(100) NOT NULL,
    dosage VARCHAR(100),
    instructions TEXT,
    FOREIGN KEY (appointment_id) REFERENCES Appointments(appointment_id)
);





🖥️HOW TO RUN
With GitHub Actions (as in your workflow files)
If you're using a GitHub repository and CI setup:
- Place your .sql scripts in .github/workflows/.
- Make sure your workflow YAML file includes steps like:
- name: Execute demo.sql
  run: mysql -u root -proot salesDB < ./.github/workflows/demo.sql
- Push your changes and GitHub will auto-run the test workflow


ENTITY RELATION DIAGRAM
![Screenshot 2025-06-30 123602](https://github.com/user-attachments/assets/ba3975f6-55db-4454-a6c8-62c8060b6c46)
