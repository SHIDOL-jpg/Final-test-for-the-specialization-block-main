### Создание базы данных

_Команда в терминале на Linux_
```sh
sudo mysql
```

_Создаём базу данных Human_Friends_
```sh
CREATE DATABASE Human_Friends;
USE Human_Friends;
```

### Создание таблиц

_Таблица Pets_
```sh
CREATE TABLE Pets (
    ID INT AUTO_INCREMENT PRIMARY KEY,
    Name VARCHAR(50),
    Type VARCHAR(50),
    BirthDate DATE,
    Commands TEXT
);
```

_Таблица PackAnimals_
```sh
CREATE TABLE PackAnimals (
    ID INT AUTO_INCREMENT PRIMARY KEY,
    Name VARCHAR(50),
    Type VARCHAR(50),
    BirthDate DATE,
    Commands TEXT
);
```

### Заполнение таблиц данными

_Заполнение таблицы Pets_
```sh
INSERT INTO Pets (Name, Type, BirthDate, Commands) VALUES
('Fido', 'Dog', '2020-01-01', 'Sit, Stay, Fetch'),
('Whiskers', 'Cat', '2019-05-15', 'Sit, Pounce'),
('Hammy', 'Hamster', '2021-03-10', 'Roll, Hide'),
('Buddy', 'Dog', '2018-12-10', 'Sit, Paw, Bark'),
('Smudge', 'Cat', '2020-02-20', 'Sit, Pounce, Scratch'),
('Peanut', 'Hamster', '2021-08-01', 'Roll, Spin'),
('Bella', 'Dog', '2019-11-11', 'Sit, Stay, Roll'),
('Oliver', 'Cat', '2020-06-30', 'Meow, Scratch, Jump');
```

_Заполнение таблицы PackAnimals_
```sh
INSERT INTO PackAnimals (Name, Type, BirthDate, Commands) VALUES
('Thunder', 'Horse', '2015-07-21', 'Trot, Canter, Gallop'),
('Sandy', 'Camel', '2016-11-03', 'Walk, Carry Load'),
('Eeyore', 'Donkey', '2017-09-18', 'Walk, Carry Load, Bray'),
('Storm', 'Horse', '2014-05-05', 'Trot, Canter'),
('Dune', 'Camel', '2018-12-12', 'Walk, Sit'),
('Burro', 'Donkey', '2019-01-23', 'Walk, Bray, Kick'),
('Blaze', 'Horse', '2016-02-29', 'Trot, Jump, Gallop'),
('Sahara', 'Camel', '2015-08-14', 'Walk, Run');
```

### Удаление записей о верблюдах и объединение таблиц лошадей и ослов

_Удаление верблюдов_
```sh
DELETE FROM PackAnimals WHERE Type = 'Camel';
```

_Объединение таблиц лошадей и ослов_
```sh
CREATE TABLE Combined_Animals AS
SELECT ID, Name, Type, BirthDate, Commands FROM PackAnimals WHERE Type IN ('Horse', 'Donkey');
```

### Создание таблицы для животных в возрасте от 1 до 3 лет и вычисление их возраста

```sh
CREATE TABLE Young_Animals AS
SELECT ID, Name, Type, BirthDate, Commands,
       TIMESTAMPDIFF(MONTH, BirthDate, CURDATE()) AS AgeMonths
FROM Pets
WHERE TIMESTAMPDIFF(YEAR, BirthDate, CURDATE()) BETWEEN 1 AND 3;
```

### Объединение всех созданных таблиц в одну

```sh
CREATE TABLE All_Animals AS
SELECT ID, Name, Type, BirthDate, Commands, 'Pets' AS Source
FROM Pets
UNION ALL
SELECT ID, Name, Type, BirthDate, Commands, 'PackAnimals' AS Source
FROM PackAnimals
WHERE Type IN ('Horse', 'Donkey');
```

### Выход из программы MySQL

```sh
exit
```
