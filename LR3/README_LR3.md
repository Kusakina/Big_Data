В данной лабораторной работе необходимо было выполнить предложенные задания (см ниже).

# Ход работы:
1. скачиваем репозиторий и прописываем путь к скачанным файлам

![image](https://github.com/Kusakina/Big_Data/assets/74459357/90369009-0ab7-4d8c-a3e6-7fc1c078e3ce)


2. Выполняем задание RideCleansingExercise, согласно инструкции к нему

  The task of the "Taxi Ride Cleansing" exercise is to cleanse a stream of TaxiRide events by removing events that start or end outside of New York City.
  Написанная функция проверяет условие начала и завершения поездки в New York City.

  ![image](https://github.com/Kusakina/Big_Data/assets/74459357/8f264809-64eb-4c5c-a805-1f9514a38342)

  ![image](https://github.com/Kusakina/Big_Data/assets/74459357/a8d9df63-10e9-4a19-b499-6460f9b77d53)

3.  Выполняем задание RidesAndFaresExercise, согласно инструкции к нему

  The goal of this exercise is to join together the TaxiRide and TaxiFare records for each ride.
  Метод open сохраняет TaxiRide и TaxiFare State в соответствующие переменные.
  В методе flatMap1 сохраняем значение faresState.value(), если оно не налл, fareState сбрасывается, генерируется новый tuple.
  В методе flatMap2 сохраняем значение ridesState.value(), если оно не налл, генерируется новый tuple, rideState сбрасывается.

![image](https://github.com/Kusakina/Big_Data/assets/74459357/35c90e5e-7922-4586-b9e9-5519839cb062)


4. Выполняем задание HourlyTipsExerxise, согласно инструкции к нему

  The task of the "Hourly Tips" exercise is to identify, for each hour, the driver earning the most tips.
  It's easiest to approach this in two steps: first use hour-long windows that compute the total tips for each driver during the hour,
  and then from that stream of window results, find the driver with the maximum tip total for each hour.
  Переписываем метод process, так, чтобы в нем считались чаевые водителя за каждый час.
  Производим группировку TaxiFare по id водителя, потом производим группировку данных по каждому часу для каждого водителя.
  Расчитываем суммму чаевых для каждого водителя за каждый час.
  Выводим найденные значения, соответствующие максимуму за каждый час работы.

  ![image](https://github.com/Kusakina/Big_Data/assets/74459357/eb826f11-2893-43a8-af3c-6c769b059bb9)


5. Выполняем задание ExpiringStateExercise, согласно инструкции к нему

  The goal of the "Long Ride Alerts" exercise is to provide a warning whenever a taxi ride lasts for more than two hours.
  Метод open сохраняет TaxiRide и TaxiFare State в соответствующие переменные.
  Метод onTimer проверяет наличие (событие не налл) fareState.value() и rideState.value(), если таковые нашлись, они передаюся в unmatchedFares или unmatchedRides, переменные для хранения сбрасываются.
  Метод processElement1 проверяет наличие (событие не налл) fareState.value(), если оно есть, сбрасывается таймер, генерируется новый tuple, переменные для хранения fareState сбрасываются,
  если значение не нашлось (оно налл), значение rideState обновляется, регистрируется таймер.
  Метод processElement2 работает аналогично методу processElement1

  ![image](https://github.com/Kusakina/Big_Data/assets/74459357/989ca7ca-4ba2-403e-b8aa-d5c896469630)

  Код методов представлен в соответствующих файлах.

