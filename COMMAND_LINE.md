
## 
### Reset device via [nrfjprog](https://www.nordicsemi.com/?sc_itemid=%7B56868165-9553-444D-AA57-15BDE1BF6B49%7D)
### Сброс устройства при помощи [nrfjprog](https://www.nordicsemi.com/?sc_itemid=%7B56868165-9553-444D-AA57-15BDE1BF6B49%7D)
  
  ```
  nrfjprog --reset -f nrf52
  ```

## 
### Erasing code and UICR flash areas via [nrfjprog](https://www.nordicsemi.com/?sc_itemid=%7B56868165-9553-444D-AA57-15BDE1BF6B49%7D)
### Стирание кода и областей флеш памяти UICR при помощи [nrfjprog](https://www.nordicsemi.com/?sc_itemid=%7B56868165-9553-444D-AA57-15BDE1BF6B49%7D)
  
* ```
  nrfjprog --recover -f NRF52
  ```

* ```
  nrfjprog -e -f nrf52
  ```
## 
### Flashing the Bootloader via [nrfjprog](https://www.nordicsemi.com/?sc_itemid=%7B56868165-9553-444D-AA57-15BDE1BF6B49%7D)
### Прошивка загрузчика при помощи [nrfjprog](https://www.nordicsemi.com/?sc_itemid=%7B56868165-9553-444D-AA57-15BDE1BF6B49%7D)

  ```
  nrfjprog -f nrf52 --program <Bootloader Name>.hex -r
  ```
  
  Example
  
  Пример
  
  ```
  nrfjprog -f nrf52 --program nrf52840_xxaa_s140.hex -r
  ```
  
## 
### Flashing the Bootloader via [AdaLink](https://github.com/adafruit/Adafruit_Adalink)
### Прошивка загрузчика при помощи [AdaLink](https://github.com/adafruit/Adafruit_Adalink)

  ```
  adalink nrf52832 -p jlink -w
  adalink nrf52832 -p jlink -h <Bootloader Name>.hex
  ```
  
## 
### Flashing the Bootloader with Softdevice via [nrfjprog](https://www.nordicsemi.com/?sc_itemid=%7B56868165-9553-444D-AA57-15BDE1BF6B49%7D)

Warrning:
In SDK 15.3 the bootloader start address is stored in the MBR section instead of the UICR (since UICR cannot be protected by ACL/BPROT), and that causes problem in the makefile, where the nrfjprog command sectorerase is used.

If you take a look at the makefile of the BLE DFU bootloader examples, you can see that the bootloader is flashed first, and the bootloader start address is stored in the MBR section. Then the Softdevice is flashed onto the chip using nrfjprog and the sectorerase command. The problem here is that sectorerase command will erase the bootloader start address before flashing the MBR.

### Прошивка загрузчика и Softdevice при помощи [nrfjprog](https://www.nordicsemi.com/?sc_itemid=%7B56868165-9553-444D-AA57-15BDE1BF6B49%7D)
В SDK 15.3 начальный адрес загрузчика хранится в разделе MBR вместо UICR (поскольку UICR не может быть защищен ACL / BPROT), и это вызывает проблему в файле makefile, где используется команда sectorerase nrfjprog

Если вы посмотрите на makefile примеров загрузчика DFU BLE, вы увидите, что загрузчик сначала прошивает, а начальный адрес загрузчика хранится в разделе MBR. После этого Softdevice прошивается на чип используя nrfjprog и команду erase участка. Проблема здесь в том, что команда Sector erase удалит начальный адрес загрузчика перед прошивкой MBR.

* Flashing the bootloader and softdevice separately

  Перепрошивки загрузчика и softdevice отдельно
  
  Example
  
  Пример
  
  ```
  nrfjprog -f nrf52 --program s140_nrf52_6.1.0_softdevice.hex --chiperase
  nrfjprog -f nrf52 --program nrf52840_xxaa_s140.hex -r
  ```
  
* Flashing the bootloader and softdevice through a merge

  Перепрошивки загрузчика и softdevice через слияние
  
  Example
  
  Пример
  ```
  mergehex -m s132_nrf52_6.1.1_softdevice.hex nrf52832_xxaa_s132.hex -o merge.hex
  ```
  
## 
### Create a firmware image using [nrfutil](https://github.com/NordicSemiconductor/pc-nrfutil)
### Создание образа микропрограммы с помощью [nrfutil](https://github.com/NordicSemiconductor/pc-nrfutil)
  
* SDK 15.3 *Using the key to secure DFU*

  SDK 15.3 *С использованием ключа для secure DFU* 
  
  Example for Softdevice s132_nrf52_6.1.1
  
  Пример для Softdevice s132_nrf52_6.1.1
  ```
  nrfutil pkg generate --hw-version 52 --sd-req 0xB7 --application-version 5 --application app.hex --key-file key.pem app_dfu_package.zip
  ```
  
## 
### Create a private (signing) key and save it in a PEM file [nrfutil](https://github.com/NordicSemiconductor/pc-nrfutil)
### Создать закрытый (подписывающий) ключ и сохранить его в файле в формате PEM с помощью [nrfutil](https://github.com/NordicSemiconductor/pc-nrfutil)
  
  ```
  nrfutil keys generate private.pem
  ```
  
## 
### Display the public key in code format from the key file (signing) key and save it in a PEM file [nrfutil](https://github.com/NordicSemiconductor/pc-nrfutil)
### Отображение открытого ключа в формате кода из файла ключа [nrfutil](https://github.com/NordicSemiconductor/pc-nrfutil)
  
  ```
  nrfutil keys display --key pk --format code private.pem
  ```
