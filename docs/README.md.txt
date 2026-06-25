Gyro — Robot Balansujący (Odwrócone Wahadło)

Projekt zespołowy realizowany na Wydziale Mechanicznym Politechniki Białostockiej. Celem projektu jest stworzenie autonomicznego robota balansującego na dwóch kołach, wykorzystującego fuzję danych z czujnika IMU oraz regulator o strukturze PD.

Wymagania Sprzętowe (Hardware)
* Mikrokontroler: Arduino Nano
* Czujnik inercyjny: IMU MPU-6050 (komunikacja I2C)
* Sterownik silników: Pololu Motoron M2T550 Dual I2C
* Napęd: 2x Silnik DC z przekładnią 25GA-370 (enkodery sprzętowe obecnie niewykorzystywane w pętli)
* Zasilanie: Pakiet 4 ogniw Li-Ion 18650 (konfiguracja 4S) z modułem BMS 40A (napięcie nominalne 14,8 V, napięcie pełne 16,8 V)

Wymagania Programowe (Software)
* Środowisko Arduino IDE (testowano na wersji 2.3+)
* Biblioteka `Wire.h` (wbudowana, do obsługi I2C 400kHz)
* Biblioteka `Motoron.h` (do pobrania z Menedżera Bibliotek, dostarczana przez Pololu)

Instrukcja Pierwszego Uruchomienia
1. Zasilanie i bezpieczeństwo: Upewnij się, że pakiet Li-Ion jest naładowany (max 16,8 V). Nie włączaj zasilania, gdy robot leży płasko.
2. Ustawienie początkowe: Ustaw robota na płaskiej i twardej powierzchni. Trzymaj ramię robota idealnie pionowo i nieruchomo.
3. Włączenie (Kalibracja): Przełącz główny włącznik zasilania. Mikrokontroler rozpocznie sprzętową autokalibrację przesunięć (offsetów) czujnika MPU-6050. Proces trwa około 3 sekund.
4. Start balansu: Po zakończeniu kalibracji (w konsoli szeregowej pojawi się komunikat "Gotowy!"), delikatnie puść ramię robota. Układ automatycznie zamknie pętlę sprzężenia zwrotnego i zacznie balansować.
5. System Fail-Safe (Zabezpieczenie przed upadkiem): Jeśli wychylenie przekroczy 35°, zasilanie silników zostanie natychmiastowo odcięte. Aby zrestartować stabilizację, należy ręcznie spionizować robota (kąt błędu < 5°).