# Домашнее задание к занятию 12.1 "`Базы данных`" - `Selivanov Sergey`


### Задание 1

Таблицы:

1. Employees (Сотрудники)
id (PK) — уникальный идентификатор
last_name — Фамилия (50)
first_name — Имя (50)
patronymic — Отчество (50)
position_id (FK) → Positions(id)
department_id (FK) → Departments(id)
hire_date — дата принятия на работу
salary — оклад (DECIMAL)

`Код:`
```
CREATE TABLE Employees (
    id SERIAL PRIMARY KEY,
    last_name VARCHAR(50) NOT NULL,
    first_name VARCHAR(50) NOT NULL,
    patronymic VARCHAR(05),
    position_id INTEGER REFERENCES Positions(id),
    department_id INTEGER REFERENCES Departments(id),
    hire_date DATE NOT NULL,
    salary DECIMAL(10,2) NOT NULL CHECK (salary > 0)
);
```

2. Positions (Должности)
id (PK)
title — название должности

`Код:`
```
CREATE TABLE Positions (
    id SERIAL PRIMARY KEY,
    title VARCHAR(150) NOT NULL UNIQUE
);
```

3. Departments (Подразделения)
id (PK)
name — название подразделения
type_id (FK) → DepartmentTypes(id)
branch_id (FK) → Branches(id)

`Код:`
```
CREATE TABLE Departments (
    id SERIAL PRIMARY KEY,
    name VARCHAR(200) NOT NULL,
    type_id INTEGER REFERENCES DepartmentTypes(id),
    branch_id INTEGER REFERENCES Branches(id)
);
```

4. DepartmentTypes (Типы подразделений)
id (PK)
name — название типа

`Код:`
```
CREATE TABLE DepartmentTypes (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL UNIQUE
);
```


5. Branches (Филиалы)
id (PK)
address — адрес филиала

`Код:`
```
CREATE TABLE Branches (
    id SERIAL PRIMARY KEY,
    address TEXT NOT NULL
);
```

6. Projects (Проекты)
id (PK)
name — название проекта

`Код:`
```
CREATE TABLE Projects (
    id SERIAL PRIMARY KEY,
    name VARCHAR(200) NOT NULL UNIQUE
);
```

7. ProjectAssignments (Назначения на проекты)
employee_id (FK) → Employees(id)
project_id (FK) → Projects(id)
assignment_date — дата назначения

`Код:`
```
CREATE TABLE ProjectAssignments (
    employee_id INTEGER REFERENCES Employees(id),
    project_id INTEGER REFERENCES Projects(id),
    assignment_date DATE DEFAULT CURRENT_DATE,
    PRIMARY KEY (employee_id, project_id)
);
```

![Схема БД](https://github.com/sergey-selivanov-png/SQL/blob/main/image/d1.png)

---
