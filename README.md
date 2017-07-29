# iot_test
# Abstract-
	The aim of the project is to acquire sensor data of accelerometer on 
	STM32 board through I2C bus and send this data to Raspberry Pi. 
	The communication between the two boards is done via Wi-Fi module(ESP8266).	 
	The data received on the Raspberry Pi will be sent to a broker via MQTT protocol. 
	One needs to subscribe to the broker for the access to data.




1) The project is about getting Accelerometer sensor data from stm32f303
   (discovery) via I2C bus and send that data to esp8266(wifi module) 
   via UART.

-> code for the above pprocedure
   (/PROJECT_DETAILS-GRP13/CODE_PROJECT/STM_SIDE_CODE/UART+I2C/uart.c)

   we configured UART1 = (PORTC(5)-RX,PORTC(4)-TX) and
	      I2C1  = (PORTB(6)-SCL,PORTB(7)-SDA).

2) The Wi-fi module which is receiving the data(STATION one) through UART
   will send the data to another wi-fi module(ACCESS POINT) via TCP/IP 
   which is connected to Raspberry Pi via UART. Whatever the data that
   Access point is receiving from station will be passed to the serial 
   port of UART.

-> code for the above procedure
   a) client
      (/PROJECT_DETAILS-GRP13/CODE_PROJECT/LUA_CODE_FOR_2_ESP's/Client(STATION)/client.txt)
   b) server
      (/PROJECT_DETAILS-GRP13/CODE_PROJECT/LUA_CODE_FOR_2_ESP's/Server(ACCESS_POINT)/server.txt)

3) Finally the data which are received at Raspberry pi's serial port  will be taken 
   into buffer and will be published to MQTT broker(Since we had no access to any MQTT broker
   so we ended up with creating a local TCP server and published the data to that server).
   In future if you have any access to Mqtt broker follow the below steps.
   
-> codes for the above procedure
   a) Publisher
      (/PROJECT_DETAILS-GRP13/CODE_PROJECT/Rpi_SIDE_CODE/Publisher/FINAL_RPI_SIDE_CODE.c)
   b) Broker
      (//PROJECT_DETAILS-GRP13/CODE_PROJECT/Rpi_SIDE_CODE/Broker/server.c)

   In future if you have any access to Mqtt broker follow the below steps.
       
	step 1)  Change the ip from 127.0.0.1 in FINAL_RPI_SIDE_CODE.c to any MQTT broker ip like(test.mosquitto.org)
	step 2)  change the port number from 8080 to 1883.
	step 3)  Once the setup is done one has to subscribe the data which are getting published from Rpi.
		 one has to give the topic name to subscribe that data as mentioned in publish packet in FINAL_RPI_SIDE_CODE.c
		 topic name- CDAC/ASAP/A.  	 
		 example- From MyMQTT android app there will be an option for subscription. once u enter the topic name you will get 
	                  the messages which are published by Raspberry pi in dashboard option.
        



*--------------------------------------------------------THANK             YOU--------------------------------------------------*
