
## 
### Board with microcontroller hangs from finger touch or hangs randomly 
### Плата с микроконтроллером зависает от прикосновения пальца или зависает случайно


* If you're using a *UART*, the reason could be that the pin of the *RX* microcontroller is "hanging in the air".
  Solution: connect the RX pin to positive power.
  
  Если вы используете *UART*, причина может быть в том, что ножка микроконтроллера *RX* "висит в воздухе".
  Решение: подтяние ножку RX к плюсу питания.
  
  ```C++
  nrf_gpio_cfg_input(UART_RX_PIN, NRF_GPIO_PIN_PULLUP);
  ```
  
* If you use *UART* without low frequency quartz and use printf.
  Solution: Select file *sdk_config.h* specified settings.
  Если вы используете *UART* без низкочастного кварца и вызываете printf.
  Решение: Выберите в файле *sdk_config.h* указанные настройки.
  
  *SDK 15.3 sdk_config.h*
  ```C++
  // <o> NRF_SDH_CLOCK_LF_SRC  - SoftDevice clock source.

  // <0=> NRF_CLOCK_LF_SRC_RC 
  // <1=> NRF_CLOCK_LF_SRC_XTAL 
  // <2=> NRF_CLOCK_LF_SRC_SYNTH 

  #ifndef NRF_SDH_CLOCK_LF_SRC
  #define NRF_SDH_CLOCK_LF_SRC 0
  #endif

  // <o> NRF_SDH_CLOCK_LF_RC_CTIV - SoftDevice calibration timer interval. 
  #ifndef NRF_SDH_CLOCK_LF_RC_CTIV
  #define NRF_SDH_CLOCK_LF_RC_CTIV 4
  #endif
  
  // <o> NRF_SDH_CLOCK_LF_ACCURACY  - External clock accuracy used in the LL to compute timing.
 
  // <0=> NRF_CLOCK_LF_ACCURACY_250_PPM 
  // <1=> NRF_CLOCK_LF_ACCURACY_500_PPM 
  // <2=> NRF_CLOCK_LF_ACCURACY_150_PPM 
  // <3=> NRF_CLOCK_LF_ACCURACY_100_PPM 
  // <4=> NRF_CLOCK_LF_ACCURACY_75_PPM 
  // <5=> NRF_CLOCK_LF_ACCURACY_50_PPM 
  // <6=> NRF_CLOCK_LF_ACCURACY_30_PPM 
  // <7=> NRF_CLOCK_LF_ACCURACY_20_PPM 
  // <8=> NRF_CLOCK_LF_ACCURACY_10_PPM 
  // <9=> NRF_CLOCK_LF_ACCURACY_5_PPM 
  // <10=> NRF_CLOCK_LF_ACCURACY_2_PPM 
  // <11=> NRF_CLOCK_LF_ACCURACY_1_PPM 

  #ifndef NRF_SDH_CLOCK_LF_ACCURACY
  #define NRF_SDH_CLOCK_LF_ACCURACY 1
  #endif
  ```
  
  ```C++
  
  ```
