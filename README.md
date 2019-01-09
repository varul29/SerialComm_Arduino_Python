# Serial-Comm-_Arduino_Python
Start your basics with serial communication which help you to read the data from any kind of sensor connected to arduino using UART, I2C, SPI or any kind of protocol

In this Repository you will understand about how can you write your own code and run it on Desktop without of using specialized IDE.
Being a newbie to IoT world and with ongoing development languages, I am going to use Python which to make this tough work to convert just in few hours only. 

## Hardware Used

  - Wireless Temperature and Humidity Sensor
  - Wireless Modem
  - Arduino Uno 
  
Using Wireless Sensor manual I was able to understand how to play with registers which give the information in bytes format just like the way we read sensor datasheets to use a different protocol like SPI, I2C or UART.

## Significance

- If I start saying about these wireless sensors, then this is one of the greatest achievement which adapt the Industrial Environment.
- With all new extreme features to work with IoT applications
- The basic start to use in the industrial  predictive system
- The application for these kind sensors will widely be used with different applications like Food Storage services, Shipping Transportation Service, Environment Analysis in manufacturing companies like Pharmaceuticals, petroleum, mining industries, and many other various industries.
- With the help of its long-range communication using 900hp-S3-pro device, it has the advantage to communicate with your device from the longer distances within your private network which basically we learned in networking related wired LAN protocol used in corporate industries.
- The era of these kind wireless sensor network is going to be the best one in major Remote area network as well as in private network.
- Being similarly working with IEEE standards 802.11.x.x these devices can work without any kind of interference with dual AA batteries only.

## Receiving the data from Arduino and Wireless Modem

While writing the code  in embedded c to receive the data of wireless sensor through a wireless modem, I am using the Sensor Manual and by understanding the register information and with help of Arduino UNO and Arduino IDE software, I am able to read the 
Sensor by using the suggested  code




- Taking bytes array for storing the information we are getting from wireless sensor

      uint8_t data[29];

- Beginning the serial communication setup 
		
		void setup()
      {	
 		   Serial1.begin(9600);
  	   Serial.begin(9600);
  	   Serial.println("ncd.io IoT Arduino wireless temperature Humidity sensor");
		  }

- Will check out the availability of different registers information availability through serial.available.

      void loop()
      {
      if (Serial1.available())
      {
        data[0] = Serial1.read();
        delay(k);
      if(data[0]==0x7E)
      {
      while (!Serial1.available());
        for ( i = 1; i< 29; i++)
        {
        data[i] = Serial1.read();
        delay(1);
        }
      if(data[15]==0x7F)  /////// to check if the recive data is correct
        {
        if(data[22]==1)  //////// make sure the sensor type is correct
        { 
	     }

- Manipulate the information which is stored in bytes array with the suggested function

      float humidity = ((((data[24]) * 256) + data[25]) /100.0);
      int16_t cTempint = (((unit16_t)(data[26])<<8)| data[27];
      float cTemp = (float)cTempint /100.0;
      float fTemp = cTemp * 1.8 + 32;
      float battery = ((data[18] * 256) + data[19]);
      float voltage = 0.00322 * battery;
  

- Finally after reading the values of wireless sensor print the values to test in Arduino serial monitor.

      Serial.print("Relative Humidity :");
      Serial.print(humidity);
      Serial.println(" %RH");
      Serial.print("Temperature in Celsius :");
      Serial.print(cTemp);
      Serial.println(" C");
      Serial.print("Temperature in Fahrenheit :");
      Serial.print(fTemp);
      Serial.println(" F");
  
## Installing Python 

To install the Python in windows you can go to python.org and, 

- Install the latest python software as I have used Python 3.6.5 version. 
- For Serial communication use, the pyserial library which is the available pyserial web page  

## Install the Pyserial Package

To install pyserial open Windows, MAC, Linux Operating system command prompt

- For  Windows  users:

      sudo python setup.py install

- For MAC and Linux use : 

      $ tar -xzf pyserial-2.6.tar.gz

## Receiving the Sensor Data in Python Shell

For the safety purpose, I am using Arduino IDE. For sensor connection between the wireless sensor and Arduino let’s use UART  connection and use Python code in Python IDLE for reading the serial data in Python shell.


    import serial
	  ard = serial.Serial('COM4', 9600);
	  While true:
      k = ard.readline().decode('ascii');	
      print(k)	

With these Simple few lines I was able to read the data continuously 

## About the python Code 
	
- Import serial package which helps us to read the sensor data from Arduino.
		
      import serial

- Using serial.Serial from pyserial in which we are initializing the Com port, Baudrate. Else than that we can also set the parity bits and many other different parameters to receive the data from Arduino.

      ard = serial.Serial('COM4', 9600);

- Using readline() object in pyserial we are reading all the data display in Arduino UNO and printing the values.
			
	  k = ard.readline().decode('ascii');
		print(k)

## Python Shell Output

Just for the testing of this of this great device, I am trying to display the values of humidity, Celsius, Fahrenheit only.


