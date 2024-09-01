# Инструкция по сборке робота с AI-модулем голсового управления на Aruduino

   Пошаговая инструкция по сборке робота, который способен выполнять голосовые команды благодаря специальному модулю голосового управления с искусственным интеллектом, распознающего команды на русском языке.
   В инструкции подробно рассказано, как собрать и запрограммировать такого робота.

## Содержание
1. [Сборка корпуса робота](#1-Сборка-корпуса-робота)
   - [Подготовка инструментов и деталей](#11-Подготовка-инструментов-и-деталей)
   - [Установка моторчиков](#12-Установка-моторчиков)
   - [Сборка колёс](#13-Сборка-колёс)
   - [Установка верхней части](#14-Установка-верхней-части)
2. [Написание скетча](#2-Написание-скетча)
   - [Подготовка к написанию кода](#21-Подготовка-к-написанию-кода)
   - [Написаниие кода](#22-Написаниие-кода)
   - [Итоговый код](#23-Итоговый-код)
   - [Перенос кода на Arduino](#24-Перенос-кода-на-Arduino)
3. [Сборка логической части робота](#3-Сборка-логической-части-робота)
   - [Подготовка инструментов и деталей](#31-Подготовка-инструментов-и-деталей)
   - [Подключение моторчиков](#32-Подключение-моторчиков)
   - [Подключение источника питания к L298N](#33-Подключение-источника-питания-к-L298N)
   - [Подключение голсового модуля к Arduino](#34-Подключение-голсового-модуля-к-Arduino)
   - [Подключение логической части к L298N](#35-Подключение-логической-части-к-L298N)
   - [Итоговый вид](#36-Итоговый-вид)

## 1 Сборка корпуса робота
### 1.1 Подготовка инструментов и деталей
   Набор корпуса включает в себя следующий список деталей:
  
   - 2 платформы корпуса
   - 4 моторчика
   - 4 колеса
   - 4 диска-енкодера
   - 8 крепежей для моторчиков
   - 12 обычных винтов
   - 8 длинных винтов
   - 8 гаек
   - 6 стоек

   ![details](https://github.com/user-attachments/assets/50ad3057-91b9-44c3-9f6f-28900af01800)

   Из инструментов нам будет достаточно крестовой отвёртки и гаечного ключа соответствующих размеров.
  
### 1.2 Установка моторчиков
   Детали для даннного этапа:
  
   - 1 платформа
   - 4 моторчика
   - 8 крпежей для моторчика
   - 8 длинных винтов
   - 8 гаек

   В первую очередь нам нужно взять платформу и найти следующие отверстия и вырезы для крепежей моторчиков.
    
   ![platform](https://github.com/user-attachments/assets/85c5d3f9-1b28-4cf6-a5e2-b9a4ea9a06ee)

   Далее мы берём один из крепежей и вставляем широкой частью вниз в указанное на рисунке выше отверстие платформы.
   Подставляем к вставленному крепежу моторчик и берём второй крепёж, который сопоставляем с указанным выше вырезом.
   Сопоставляем отверстия на крепежах и моторе и затем вставляем в них длинные винты. Закрепляем винты гайками при помощи гаечного ключа.
  
   ![bolts](https://github.com/user-attachments/assets/c7244cb8-2405-4f5d-b270-91391fe1168d)

   Установка одного моторчика закончена, теперь нужно закрепить остальные три моторчика аналогичным способом.
  
### 1.3 Сборка колёс
   Сборку колёс мы начнём с установки дисков-энкодеров. Они устанавливаются с внутренней стороны вращательного элемента моторчика.
  
![encoders](https://github.com/user-attachments/assets/14cf53dc-bcc6-4503-850c-abcb057af891)

   Теперь мы установим сами колёса. Сопоставим отверстия на самих колёсах и на моторчиках.

   ![wheels](https://github.com/user-attachments/assets/c496d7fe-ba5c-4770-8601-31a83c646256)

### 1.4 Установка верхней части
   Последним этапом сборки является установка верхней платформы. Для её установки нам понадобится:

   - 6 стоек
   - 12 обычных винтов
   - 1 платформа корпуса

   Стойки нужно закрепить винтами при помощи крестовой отвёртки в следующие отверстия на платформе с моторчиками:

   ![stands_platform](https://github.com/user-attachments/assets/be3a76db-a316-44e6-8214-151867520bb4)

   Стойки, прикрученные к платформе с моторчиками:
   
   ![stands](https://github.com/user-attachments/assets/15064e04-da6d-473e-96ca-eddd799e834c)

   Теперь остаётся взять верхнюю платформу, сопоставить её с отверстиями для стоек и закрепить винтами.

   ![top_platform](https://github.com/user-attachments/assets/bfb9040e-58df-443f-a081-fe93f7316685)

## 2 Написание скетча
### 2.1 Подготовка к написанию кода
   Для того чтобы начать написание кода для Arduino, нам нужно установить драйвер для платы, а также специальную среду разработки Arduino IDE с официального сайта производителя.
  
   [Ссылка на драйвер Arduino UNO](https://iarduino.ru/file/126.html)
  
   [Ссылка на Arduino IDE](https://www.arduino.cc/en/software)
  
### 2.2 Написаниие кода
   Теперь, когда мы установили всё нужное программное обеспечение для написания кода, мы открываем Arduino IDE и нажимаем на кнопку создания нового скетча.
   
   Сначала нам стоит определиться, каким образом Arduino будет принимать информацию с голосового модуля.
   Есть три способа:
  
   - UART
   - I2C
   - SPI

   Для наших задач нам больше всего подойдёт UART или I2C, так как они просты в подключении и требуют меньше проводов, чем SPI.
   В данной инструкции мы будем рассматривать подключение через I2C, так как передача данных по нему быстрее, чем на UART, а также данный тип подключения поддерживает связь с несколькими устройствами на одной шине.
   Это позволяет легко подключить несколько датчиков, модулей или контроллеров на одной линии (SDA и SCL), что экономит количество проводов и упрощает схему.

   Чтобы Arduino смогла читать данные через I2C, нужно его подключить, а также прописать порты, через которые Arduino будет передавать сигналы моторчикам.

   ```
   #define ESP_SLAVE_ADDR 0x36
   #include <Wire.h>
   
   const int in1 = 7; // Пин движения вперёд для колёс с правой стороны
   const int in2 = 6; // Пин движения назад для колёс с правой стороны (+ШИМ)
   const int in3 = 5; // Пин движения вперёд для колёс с левой стороны (+ШИМ)
   const int in4 = 4; // Пин движения назад для колёс с левой стороны
   
   void setup() {
     Wire.begin(ESP_SLAVE_ADDR);   // Устанавливаем адрес slave устройства I2C
     Wire.onReceive(receiveEvent); // Устанавливаем обработчик для события получения данных
     Serial.begin(9600);           // Настраиваем Serial для вывода логов
   
     // Инициализируем пины для управления двигателями как выходы
     pinMode(in1, OUTPUT);
     pinMode(in2, OUTPUT);
     pinMode(in3, OUTPUT);
     pinMode(in4, OUTPUT);
   }
   
   void loop() {
     delay(100);  // Пустой цикл
   }
   ```

  Теперь мы должны прописать процесс считывания информации и распознавания команд.

   ```
   void receiveEvent(int howMany) {
     if (howMany <= 0) return;  // Проверка, есть ли данные для чтения
   
     String command = ""; // Объявление переменной для записи команды
   
     // Считываем все пришедшие символы в переменную command
     while (Wire.available() > 0) { 
       char c = Wire.read();
       command += c;  
     }
     
     // Анализируем команду и выполняем соответствующие действия
     if (command.indexOf("вперед") != -1) {
       moveForward();
     } else if (command.indexOf("назад") != -1) {
       moveBack();
     } else if (command.indexOf("старт")!= -1) {
       moveStart();
     }else if (command.indexOf("стоп") != -1) {
       stopMotors();
     } else if (command.indexOf("вправо") != -1) {
       moveRight();
     } else if (command.indexOf("влево") != -1) {
       moveLeft();
     }
   }
   ```

  Остаётся прописать сами команды, а именно какие моторы и в каком направлении нам нужно активировать при той или иной команде.
  В данном скетче мы пропишем самые основные команды: вперёд, назад, влево, вправо и стоп.
  Также добавим команду "старт", которая позволяет роботу ехать вперёд до тех пор, пока не будет сказана команда "стоп".
  
   ```
   // Движение вперед
   void moveForward() {
     digitalWrite(in1, HIGH);
     digitalWrite(in2, LOW);
     digitalWrite(in3, HIGH);
     digitalWrite(in4, LOW);
     delay(300000);
     stopMotors();
   }
   
   // Движение без остановки
   void moveStart() {
     digitalWrite(in1, HIGH);
     digitalWrite(in2, LOW);
     digitalWrite(in3, HIGH);
     digitalWrite(in4, LOW);
   }
   
   // Движение назад
   void moveBack() {
     digitalWrite(in1, LOW);
     digitalWrite(in2, HIGH);
     digitalWrite(in3, LOW);
     digitalWrite(in4, HIGH);
     delay(300000);
     stopMotors();
   }
   
   // Поворот вправо
   void moveRight() {
     digitalWrite(in1, LOW);
     digitalWrite(in2, HIGH);
     digitalWrite(in3, HIGH);
     digitalWrite(in4, LOW);
     delay(150000);
     stopMotors();
   }
   
   // Поворот влево
   void moveLeft() {
     digitalWrite(in1, HIGH);
     digitalWrite(in2, LOW);
     digitalWrite(in3, LOW);
     digitalWrite(in4, HIGH);
     delay(150000);
     stopMotors();
   }
   
   // Остановка двигателей
   void stopMotors() {
     digitalWrite(in1, LOW);
     digitalWrite(in2, LOW);
     digitalWrite(in3, LOW);
     digitalWrite(in4, LOW);
   }
   ```

   >[!TIP]
   > Помимо стандартных команд, которые прописаны в скетче, в голосовой модуль загружено распознавание таких слов, как: "домой", "быстро", "медленно" и "спать".
   >
   >Первые три команды требуют написания отдельного кода, как и для основных команд, а команда "спать" уже работает и позволяет выключить на время функцию распознования слов на голосовои модуле.
  
### 2.3 Итоговый код
   В результате мы получили скетч, который обрабатывает запросы с голосового модуля через I2C и подаёт сигналы действий на моторчики.

   ```
   #define ESP_SLAVE_ADDR 0x36
   #include <Wire.h>
   
   const int in1 = 7; // Пин движения вперёд для колёс с правой стороны
   const int in2 = 6; // Пин движения назад для колёс с правой стороны (+ШИМ)
   const int in3 = 5; // Пин движения вперёд для колёс с левой стороны (+ШИМ)
   const int in4 = 4; // Пин движения назад для колёс с левой стороны
   
   void setup() {
     Wire.begin(ESP_SLAVE_ADDR);   // Устанавливаем адрес slave устройства I2C
     Wire.onReceive(receiveEvent); // Устанавливаем обработчик для события получения данных
     Serial.begin(9600);           // Настраиваем Serial для вывода логов
   
     // Инициализируем пины для управления двигателями как выходы
     pinMode(in1, OUTPUT);
     pinMode(in2, OUTPUT);
     pinMode(in3, OUTPUT);
     pinMode(in4, OUTPUT);
   }
   
   void loop() {
     delay(100);  // Пустой цикл
   }
   
   void receiveEvent(int howMany) {
     if (howMany <= 0) return;  // Проверка, есть ли данные для чтения
   
     String command = ""; // Объявление переменной для записи команды
   
     // Считываем все пришедшие символы в переменную command
     while (Wire.available() > 0) { 
       char c = Wire.read();
       command += c;  
     }
     
     // Анализируем команду и выполняем соответствующие действия
     if (command.indexOf("вперед") != -1) {
       moveForward();
     } else if (command.indexOf("назад") != -1) {
       moveBack();
     } else if (command.indexOf("старт")!= -1) {
       moveStart();
     }else if (command.indexOf("стоп") != -1) {
       stopMotors();
     } else if (command.indexOf("вправо") != -1) {
       moveRight();
     } else if (command.indexOf("влево") != -1) {
       moveLeft();
     }
   }
   
   // Движение вперед
   void moveForward() {
     digitalWrite(in1, HIGH);
     digitalWrite(in2, LOW);
     digitalWrite(in3, HIGH);
     digitalWrite(in4, LOW);
     delay(300000);
     stopMotors();
   }
   
   // Движение без остановки
   void moveStart() {
     digitalWrite(in1, HIGH);
     digitalWrite(in2, LOW);
     digitalWrite(in3, HIGH);
     digitalWrite(in4, LOW);
   }
   
   // Движение назад
   void moveBack() {
     digitalWrite(in1, LOW);
     digitalWrite(in2, HIGH);
     digitalWrite(in3, LOW);
     digitalWrite(in4, HIGH);
     delay(300000);
     stopMotors();
   }
   
   // Поворот вправо
   void moveRight() {
     digitalWrite(in1, HIGH);
     digitalWrite(in2, LOW);
     digitalWrite(in3, LOW);
     digitalWrite(in4, HIGH);
     delay(150000);
     stopMotors();
   }
   
   // Поворот влево
   void moveLeft() {
     digitalWrite(in1, LOW);
     digitalWrite(in2, HIGH);
     digitalWrite(in3, HIGH);
     digitalWrite(in4, LOW);
     delay(150000);
     stopMotors();
   }
   
   // Остановка двигателей
   void stopMotors() {
     digitalWrite(in1, LOW);
     digitalWrite(in2, LOW);
     digitalWrite(in3, LOW);
     digitalWrite(in4, LOW);
   }
   ```
  
### 2.4 Перенос кода на Arduino
   После написания всей программы, мы можем проверить скетч на наличие ошибок с помощью встроенной системы проверки Arduino IDE.
   Для этого нужно нажать на кнопку со значком "галочка" в верхнем левом углу. Если ошибок нет, то на вкладке "Консоль" будет указано "Готово", и можно переходить к следующему шагу — переносу кода на Arduino.
   
   Для переноса кода на Arduino необходимо подключить плату к компьютеру с помощью USB-кабеля.
   После этого нужно нажать на кнопку "Upload" с изображением стрелки направленной вправо (находится рядом с кнопкой проверки кода).
   В результате этого программа загрузится на плату, и можно будет перейти к подключению логической части.

   > [!WARNING]
   > Убедитесь в том, что вы загружайте скетч на порт COM3. В противном случаем, при загрузке программа выдаст ошибку.
   > Проверить и изменить порт можно в меню рядом с кнопкой Upload в верхнем углу Arduino IDE.

## 3 Сборка логической части робота
### 3.1 Подготовка инструментов и деталей
   Логическая часть робота состоит из:

   - Плата Arduino UNO
   - Плата управления моторами L298N
   - AI-модуль голсового управления
   - Источник питания (9В батарейка или аккумулятор)
   - Провода

Из инструментов нам будет достаточно крестовой отвёртки соответствующего размера.

### 3.2 Подключение моторчиков
   В первую очередь подключаем моторчики к плате L298N следующим образом:
   - Подключаем моторчики с правой стороны к выходам L298N OUT1 и OUT2
   - Подключаем моторчики с левой стороны к выходам L298N OUT3 и OUT4

   ![Motors](https://github.com/user-attachments/assets/6e702409-39c7-4e78-8de5-9bc0e80573f2)

### 3.3 Подключение источника питания к L298N
   Теперь мы подключим источник питания к драйверу.
   Для этого на плате есть клемы 12V и GND. Подключаем плюс к 12V и минус к GND.
   Оставшуюся клему 5V мы оставим для подключения питания Arduino и голосового модуля.

   ![Power](https://github.com/user-attachments/assets/83059d02-cd3a-4de2-a9ce-6eb517b76672)

  > [!WARNING]
  > При подключении к драйверу источник питания должен быть выключен!

### 3.4 Подключение голсового модуля к Arduino
   Перед тем как подключить логическую часть к питанию, мы должны соединить голосовой модуль с Arduino для передачи команд.
   
   ![AI-Arduino](https://github.com/user-attachments/assets/32d397e0-d0d7-4eb1-a7b4-809e232b7213)


### 3.5 Подключение логической части к L298N
   Теперь можно подключить Arduino и голосовой модуль к драйверу.
   Помимо питания нам нужно будет подключить входы, которые позволят передавать команды на моторчики.
   На драйвере эти ходы обозначены как: IN1, IN2, IN3 и IN4.

   ![Arduino-L298N](https://github.com/user-attachments/assets/b3e9b5db-942b-4141-98c5-8d3e379b5a6b)

### 3.6 Итоговый вид
   В результате, мы успешно собрали робота на arduino с возможностью голосового управления.
   
   ![robot](https://github.com/user-attachments/assets/ecb86de4-d9ef-4ee6-a9fe-08e547754f5c)

## FAQ
Проект был сделан по заказу компании ООО "МИР" в 2024 году.
