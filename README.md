# programowanie2
Repozytorium do projektu ML na programowanie.

Baza danych: https://www.kaggle.com/datasets/alexteboul/heart-disease-health-indicators-dataset?select=heart_disease_health_indicators_BRFSS2015.csv
Cel: przewidzenie choroby serca lub zawału na podstawie m.in. danych zdrowotnych 253680 pacjentów.
Wartości na których model bazował to wartość ciśnienia krwi, cholesterolu, BMI, czy badany jest palaczem, czy miał udar, cukrzycę, deklarowaną aktywność fizyczną lub jej brak, spożywanie warzyw, owoców i alkoholu, dostępność służby zdrowia lub jej brak, ogólny stan zdrowia, zdrowie psychiczne i fizyczne, trudność w chodzeniu, płeć, wiek, edukacja i dochód.
Zmienna docelowa: HeartDiseaseorAttack - choroba serca lub zawał, przy czym 0 = brak ryzyka, badany zdrowy; 1 = ryzyko choroby/zawału.

Analiza danych
info(): 253680 non-null, liczba taka sama jak liczba wierszy -> nie ma brakujących danych.
describe(): mean pokazuje, że wśród badanych 9,4% ma chorobę serca lub zawał (0 = 229787 osób; 1 = 23893 osób)
(corr): największa korelacja choroby serca lub zawału z: ogólnym stanem zdrowia, wiekiem, trudnością w chodzeniu, wysokim ciśnieniem krwi i przeżytym udarem, najmniejsza z: dochodem, edukacją i deklarowaną aktywnością fizyczną.

Wyniki
Logistic Regression: accuracy = 91%; f1-score dla 0 = 0.95; dla 1 = 0.20 -> model bardzo dobrze rozpoznaje ludzi zdrowych, ale nie umie identyfikować osób chorych.
Logistic Regression z class_weight='balanced' (model będzie bardziej zwracał uwagę na 1): accuracy = 75%; f1-score dla 0 = 0.85; dla 1 = 0.38 -> znajduje więcej chorych, ale dokładność spadła.
Random Forest: accuracy = 90%; f1-score dla 0 = 0.95; dla 1 = 0.17 -> znowu model potrafi odnajdować tylko ludzi zdrowych.
Random Forest z class_weight='balanced': accuracy = 90%; f1-score dla 0 = 0.95; dla 1 = 0.15 (precision i recall też spadło) -> class_weight='balanced' tym razem nie polepszyło predykcji modelu.
Ze względu na najlepszy wynik przy użyciu Logistic Regression z class_weight='balanced' dla tego modelu szukam najleszych parametrów = {'C': 0.01}. F1-score dla 0 i 1 wyszedł taki sam jak w przypadku Logistic Regression z class_weight='balanced'. 
Z tych dwóch modeli lepszy okazał się Logistic Regression, jednak żaden nie potrafił ze skutecznością przewidzieć choroby serca lub zawału, być może ze względu na dużą przewagę w bazie osób zdrowych (91%) i niewielką ilość osób chorych (9%).
