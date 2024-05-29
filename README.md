# Arduino-Servo-Basics ![arduinoThumb](https://github.com/ICAREMAKER/Arduino-Servo-Basics/assets/107696317/2501d810-95e6-4dd2-be05-45868c0caa29) ![C++-Logo wine](https://github.com/ICAREMAKER/Arduino-Servo-Basics/assets/107696317/32c74bde-4af5-413f-81b5-8a6b8ad12a2c)



## TUTO n°1
```C
#include <Servo.h> 		// Inclure la librairie Servo.h

Servo mon_servo;    	// création de l'objet mon_servo 
int pin_servo = 6;    // Pin sur lequel est branché le servomoteur
int position = 40;    // Position souhaitée en degré

void setup() 
{
  mon_servo.attach(pin_servo);  	// attache le servo au pin spécifié sur l'objet mon_servo
  mon_servo.write(position);      // envoie la valeur (position en degré)au servomoteur mon_servo
}

void loop() {}
```

NOTA - Pour un angle de 60° :

``` mon_servo.write (60); ```

``` mon_servo.writeMicroseconds(1472); ```


## TUTO n°2
```C
#include <Servo.h>

Servo mon_servo;  	// Donner un nom au servo

int potpin = 0;  	 // Définir sur quel broche se trouve le potentiomètre
int val;    			 // Créer une variable ‘’Val’’

void setup() 
{
 mon_servo.attach(6);  	// Le servomoteur est branché sur la broche 6
}

void loop()
 {
 val = analogRead(potpin);            	// Lire la valeur du potentiomètre (valeur  entre 0 et 1023)
 val = map(val, 0, 1023, 0, 180);     	// Conversion des valeurs analogiques en degré
 mon_servo.write(val);                  // Envoyer la valeur vers le servomoteur
 delay(15);                           	// Réaliser une pause de 15 millisecondes

```
