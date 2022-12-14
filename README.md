# hctm
## Создание модели для прогнозирования макроэкономических показателей
  
Постановка задачи На основе исторических данных из нескольких сотен макроэкономических и финансовых показателей построить модель, которая сможет используя принципы метообучения адаптироваться к задачам прогнозирования новых переменных, в том числе имеющих короткую историческую длину.

### Проблема кейса:

- небольшое количество данных;
- алгоритм должен быстро адаптироваться под решение новых задач.

### Проведено небольшое исследование. Найдены варианты:
- model agnostic meta learning(maml). Данная модель хорошо справляется с задачами при небольшом объеме данных и легко адаптируется под решение новых задач. 
- нейросеть с рекуррентными слоями. Модель может работать с малыми объемами данных и предсказывать временные ряды.
- Ансамбль простых моделей с дополнительным классификатором.

Выбран второй вариант, как оптимальный по скорости  разработки и качеству работы. Код будем писать на  Python (tensorfolw, keras, pandas, numpy).

### Шаги решения:
- Из учебной выборки скроем от модели тестовую часть (последние 4 строки);
- Для обучения будем использовать ряды длиной 20, предсказываю 21точку. В каждой эпохе будем использовать 50 бачей. 
- Обучать модели будем с различными гиперпараметрами, оценивая их качество   на основе ошибки предсказания по тестовой выборке, как метрику будем использовать MSE.
- Для предсказаний выберем модель с минимальным MSE.
- Для предсказания результата обучим лучшую модель на тестовых данных и сделаем прогноз. Сохраним результат прогноза. Модель, обученную на тестовых данных в дальнейшем использовать не будем.

### Уникальность:
- Данная модель хорошо адаптируется к другим входным данным, поскольку уменьшает среднюю ошибку предсказания независимо от обучающей выборки. При увеличении объема выборки модель сохраняет свою актуальность и улучшает качество предсказания. 
- В модели не используется импортное ПО, кроме бесплатных популярных библиотек.

### Особенность:
- алгоритм нейросети LSTM способен работать в условиях малого количества обучающих данных.

### Возможное улучшение модели:
- Было отмечено, что почти все из представленных рядов можно разнести по нескольким кластерам в зависимости от их мета-характеристик. Полагаем, что обучение отдельных моделей для каждого кластера могло бы увеличить качество обучения и прогнозов.
