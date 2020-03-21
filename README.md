# PROJECT-340
CREATE DATABASE updatedProject2;
USE updatedProject2;



CREATE TABLE Ward(

Ward_ID INT(10) NOT NULL,

Ward_Name VARCHAR(60)NOT NULL ,

Ward_Location VARCHAR(100)NOT NULL,

Ward_Beds INT NOT NULL,

Ward_PhoneNumber BIGINT NOT NULL,

PRIMARY KEY (Ward_ID));


CREATE TABLE Staff(

Staff_ID INT NOT NULL,

Staff_Name VARCHAR(45) NOT NULL,

Staff_Address VARCHAR(100) NOT NULL,

Staff_PhoneNumber BIGINT NOT NULL,

Staff_DOB DATETIME NOT NULL,

Staff_Gender VARCHAR(10) NOT NULL,

Staff_NIN BIGINT NOT NULL,

Staff_Position VARCHAR(60) NOT NULL,

Staff_CurrentSalary INT NOT NUll,

Staff_SalaryScale INT NOT NUll,

PRIMARY KEY (Staff_ID));


CREATE TABLE Staff_Qualifications(

Staff_ID INT NOT NULL,

Qual_Date DATETIME,

Qual_Type VARCHAR(60),

Qual_Institution VARCHAR(60),

FOREIGN KEY(Staff_ID) REFERENCES Staff(Staff_ID));


CREATE TABLE Staff_WorkXP(

Staff_ID INT NOT NULL,

Work_Organization VARCHAR(60),

Work_Position VARCHAR(60),

Work_StartDate DATE,

Work_FinishDate DATE,

FOREIGN KEY(Staff_ID) REFERENCES Staff(Staff_ID));

    

CREATE TABLE Staff_Contract(

Staff_ID INT NOT NULL,

Contract_Type VARCHAR(1),

Contract_SalaryType VARCHAR(1),

WeeklyHoursWorked INT,

FOREIGN KEY(Staff_ID) REFERENCES Staff(Staff_ID));


CREATE TABLE Patient(

Patient_ID INT NOT NULL,

Patient_Name VARCHAR(60) NOT NULL,

Patient_Address VARCHAR(60) NOT NULL,

Patient_PhoneNumber BIGINT NOT NULL,

Patient_DOB DATE NOT NULL,

Patient_Gender VARCHAR(10),

Patient_MaritalStatus VARCHAR(10) NOT NULL,

Patient_DateRegistered DATE NOT NULL,


Patient_KinName VARCHAR(60),

Patient_KinRelationship VARCHAR(60),

Patient_KinAddress VARCHAR(60),

Patient_KinPhone BIGINT,


PRIMARY KEY(Patient_ID));


CREATE TABLE Patient_Doctor(

Patient_ID INT NOT NULL,

Doctor_Name VARCHAR(60),

Doctor_ClinicID INT NOT NULL,

Doctor_ClinicAddress VARCHAR(60),

Doctor_ClinicPhone BIGINT NOT NULL,

FOREIGN KEY (Patient_ID) REFERENCES Patient(Patient_ID));


CREATE TABLE Patient_Appointment(

Patient_ID INT NOT NULL,

Appointment_ID INT NOT NULL,

Appointment_Reservation DATETIME NOT NULL,

Appointment_RoomNumber INT NOT NULL,

Appointment_DateOnWaitingList DATETIME,

Consultant_StaffName VARCHAR(60), --

Consultant_StaffID INT NOT NULL,

FOREIGN KEY (Patient_ID) REFERENCES Patient(Patient_ID),

FOREIGN KEY (Consultant_StaffID) REFERENCES Staff(Staff_ID),

PRIMARY KEY (Appointment_ID)

);


CREATE TABLE OutPatient(

Patient_ID INT NOT NULL,

Patient_Appointment_ID INT NOT NULL,

Patient_Name VARCHAR(60), -- 

Patient_Address VARCHAR(60), -- 

Patient_PhoneNumber BIGINT, -- 

Patient_DOB DATETIME, -- 

Patient_Gender VARCHAR(60), -- 

Appointment_Reservation DATETIME, -- 

FOREIGN KEY (Patient_ID) REFERENCES Patient(Patient_ID),

FOREIGN KEY (Patient_Appointment_ID) REFERENCES Patient_Appointment(Appointment_ID)

);



CREATE TABLE InPatient(

Patient_ID INT NOT NULL,

Patient_Name VARCHAR(60) NOT NULL, --

Patient_Address VARCHAR(60) NOT NULL, --

Patient_PhoneNumber BIGINT NOT NULL, --

Patient_DOB DATE NOT NULL, --

Patient_Gender VARCHAR(60), --

Patient_MaritalStatus VARCHAR(60) NOT NULL, --

Kin_Name VARCHAR(60), --

Kin_Relationship VARCHAR(60), --

Kin_Address VARCHAR(60), --

Kin_Phone VARCHAR(60), --

Appointment_ID INT NOT NULL,

Appointment_DateOnWaitingList DATETIME, --

Ward_ID INT NOT NULL,


InPatient_ExpectedDuration INT,

InPatient_DatePlacedInWard DATE NOT NULL,

InPatient_ExpectedDepartureDate DATE,

InPatient_DateLeft DATE,

InPatient_BedID INT NOT NULL,

FOREIGN KEY (Patient_ID) REFERENCES Patient(Patient_ID),

FOREIGN KEY (Appointment_ID) REFERENCES Patient_Appointment(Appointment_ID),

FOREIGN KEY(Ward_ID) REFERENCES Ward(Ward_ID)

);



CREATE TABLE Medication(

Medication_Number INT NOT NULL,

Medication_Name VARCHAR(60) NOT NULL,

Medication_Description VARCHAR(200) NOT NULL,

Medication_UnitsPerDay INT NOT NULL,

Medication_MethodOfAdministration VARCHAR(60) NOT NULL,

Medication_StockQuantity INT,

Medication_ReorderLevel INT NOT NULL,

Medication_CostPerUnit FLOAT,

PRIMARY KEY (Medication_Number)

);


CREATE TABLE PatientMed(

Patient_ID INT NOT NULL,

Patient_Name VARCHAR(60), --

Medication_Number INT NOT NULL,

Medication_Name VARCHAR(60), --

Medication_UnitsPerDay INT, --

Medication_MethodOfAdministration VARCHAR(60), --

PatientMed_StartDate DATE NOT NULL,

PatientMed_FinishDate DATE NOT NULL,

FOREIGN KEY (Patient_ID) REFERENCES Patient(Patient_ID),

FOREIGN KEY (Medication_Number) REFERENCES Medication(Medication_Number));


CREATE TABLE SurgicalAndNonsurgicalItems(

Item_Number INT NOT NULL,

Item_Name VARCHAR(60) NOT NULL,

Item_Description VARCHAR(200) NOT NULL,

Item_StockQuantity INT,

Item_ReorderLevel INT NOT NULL,

Item_CostPerUnit FLOAT,

PRIMARY KEY (Item_Number)

);


CREATE TABLE Suppliers(

Suppliers_Number INT NOT NULL,

Suppliers_Name VARCHAR(60)  NOT NULL,

Suppliers_Address VARCHAR(60) NOT NULL,

Suppliers_Phone BIGINT,

Suppliers_Fax INT,

PRIMARY KEY (Suppliers_Number)

);


CREATE TABLE Ward_Requisition(

Requisition_Number INT NOT NULL,

Requisition_Date DATE,

Staff_ID INT NOT NULL,

Staff_Name VARCHAR(45), --

Ward_ID INT NOT NULL,

Ward_Name VARCHAR(60), --

Medication_Number BIGINT NOT NULL,

Medication_Name VARCHAR(60), --

Medication_Description VARCHAR(200), --

Medication_UnitsPerDay INT NOT NULL, --

Medication_MethodOfAdministration VARCHAR(60), --

Medication_CostPerUnit FLOAT, --

PRIMARY KEY (Requisition_Number),

FOREIGN KEY(Staff_ID) REFERENCES Staff(Staff_ID),

FOREIGN KEY(Ward_ID) REFERENCES Ward(Ward_ID),

FOREIGN KEY(Medication_Number) REFERENCES Medication(Medication_Number)

);

