USE CompanyDB;
GO

CREATE TABLE Department (
    DNUM INT PRIMARY KEY,
    DName VARCHAR(50) NOT NULL   
);
GO

CREATE TABLE Dept_Locations (
    DNUM INT NOT NULL,          
    Location VARCHAR(50),        
    PRIMARY KEY (DNUM, Location),
    FOREIGN KEY (DNUM) REFERENCES Department(DNUM)
);
GO

CREATE TABLE Employee (
    SSN CHAR(9) PRIMARY KEY,
    Fname VARCHAR(30) NOT NULL,  
    Lname VARCHAR(30) NOT NULL, 
    BirthDate DATE,              
    Gender CHAR(1),           
    DNUM INT,                
    SuperSSN CHAR(9),         
    FOREIGN KEY (DNUM) REFERENCES Department(DNUM),
    FOREIGN KEY (SuperSSN) REFERENCES Employee(SSN)
);
GO

CREATE TABLE Dept_Manager (
    DNUM INT PRIMARY KEY,
    SSN CHAR(9) NOT NULL,  
    HireDate DATE,              
    FOREIGN KEY (DNUM) REFERENCES Department(DNUM),
    FOREIGN KEY (SSN) REFERENCES Employee(SSN)
);
GO

CREATE TABLE Project (
    PNumber INT PRIMARY KEY,
    PName VARCHAR(50) NOT NULL,
    Location VARCHAR(50),        
    City VARCHAR(50),            
    DNUM INT,                   
    FOREIGN KEY (DNUM) REFERENCES Department(DNUM)
);
GO

CREATE TABLE Works_On (
    SSN CHAR(9) NOT NULL,       
    PNumber INT NOT NULL,     
    WorkingHours INT,           
    PRIMARY KEY (SSN, PNumber),
    FOREIGN KEY (SSN) REFERENCES Employee(SSN),
    FOREIGN KEY (PNumber) REFERENCES Project(PNumber)
);
GO

CREATE TABLE Dependent (
    SSN CHAR(9) NOT NULL,      
    DependentName VARCHAR(50) NOT NULL, 
    Gender CHAR(1),              in
    BirthDate DATE,              
    PRIMARY KEY (SSN, DependentName),
    FOREIGN KEY (SSN) REFERENCES Employee(SSN) ON DELETE CASCADE
);
GO

