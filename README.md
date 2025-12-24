# Arduino-Servo-Basics ![arduinoThumb](https://github.com/ICAREMAKER/Arduino-Servo-Basics/assets/107696317/2501d810-95e6-4dd2-be05-45868c0caa29) ![C++-Logo wine](https://github.com/ICAREMAKER/Arduino-Servo-Basics/assets/107696317/32c74bde-4af5-413f-81b5-8a6b8ad12a2c)

![SG90](https://github.com/ICAREMAKER/Arduino-Servo-Basics/assets/107696317/40a6efd8-04af-4d4d-af86-b2323c569537)


## TUTO n°1: Définir une position
```C
#include <Servo.h> 		// Inclure la librairie Servo.h

Servo mon_servo;    	// création de l'objet mon_servo 
int pin_servo = 6;    // Pin sur lequel est branché le servomoteur
int position = 40;    // Position souhaitée en degré

void setup() 
{
  mon_servo.attach(pin_servo);    // attache le servo au pin spécifié sur l'objet mon_servo
  mon_servo.write(position);      // envoie la valeur (position en degré)au servomoteur mon_servo
}

void loop() {}
```

NOTA - Exemple pour un angle de 60° :

``` mon_servo.write (60); ```

``` mon_servo.writeMicroseconds(1472); ```


## TUTO n°2: Modifier une position avec un potentiometre
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
## TUTO n°3: Faire varier la vitesse de rotation
![servo360](https://github.com/user-attachments/assets/522c238c-31b2-414b-86bb-8f6ee9bbe961)

```C 
#include <Servo.h>

Servo myservo1; 


void setup() {
  myservo1.attach(9);  // attache servo au pin 9
  myservo1.writeMicroseconds(1000);
  delay (1000);
}

void loop() {
  Servo1_Smooth (1000, 1500, 10); // (debut,fin,vitesse)
  delay(abs(1000-1500)*10);
}

//////////////////////////////////////////////////////////////////////
// 0°  = 1000 ms microsecondes <=> SENS ANTI-HORLOGE
//90°  = 1500 ms microsecondes <=> STOP ROTATION
//180° = 2000 ms microsecondes <=> SENS HORLOGE
/////////////////////////////////////////////////////////////////////

void Servo1_Smooth (int InitPos, int TargetPos, int Timer) { //j'integre des variables locales
static unsigned long TempsPasse = 0;
unsigned long TempsActuel = millis();
  if (TempsActuel - TempsPasse >= Timer) {
    TempsPasse = TempsActuel;
	
	if (InitPos < TargetPos) {
    InitPos++ ;
    myservo1.writeMicroseconds(InitPos); } 
	
    if (InitPos > TargetPos) {
    InitPos-- ;
    myservo1.writeMicroseconds(InitPos);
    }
```
## TUTO n°4: Définir une position avec le terminal
```C
#include <Servo.h> 		// Inclure la librairie Servo.h

Servo mon_servo;    	// création de l'objet mon_servo 
int pin_servo = 6;    // Pin sur lequel est branché le servomoteur
int position = 90;    // Position souhaitée en degré au démarage

void setup() 
{
  Serial.begin(9600);
  mon_servo.attach(pin_servo);    // attache le servo au pin spécifié sur l'objet mon_servo
  mon_servo.write(position);      // envoie la valeur (position en degré)au servomoteur mon_servo
}

void loop() {}
 if (Serial.available() > 0) {                    // Si le terminal est disponible
    long myInt = Serial.parseInt(SKIP_ALL, '\n'); // J'écris une valeur via le terminal
    mon_servo.write(myInt);			  // La position de mon servo est la valeur de mon terminal
  }
}
```
## TUTO n°5: Utiliser un TIMER
```C
#include <Servo.h>
Servo monServo;     // Crée un objet Servo
int angle = 0;      // Variable pour stocker l'angle
unsigned long TEMPSPRECEDENT_1 = 0;// Intervalle de temps en millisecondes (1 seconde)
const int INTERVALLE_1 = 1000;  // 1 seconde

void setup() {
  monServo.attach(9);
  Serial.begin(9600);
}
void loop() {
  // Récupère le temps actuel
  unsigned long TEMPSACTUEL_1 = millis();

  // --- Logique du Timer Non-Bloquant ---
  // Vérifie si l'intervalle s'est écoulé
  if (TEMPSACTUEL_1 - TEMPSPRECEDENT_1 >= INTERVALLE_1) {
    tempsPrecedent = tempsActuel; // Le temps est écoulé ! Met à jour le temps de la dernière exécution

    // 2. Exécute l'action périodique
    for (angle = 0; angle <= 180; angle += 1) {
    monServo.write(angle);  // Envoie l'angle au servomoteur
  }
    for (angle = 180; angle >= 0; angle -= 1) {
    monServo.write(angle);    
  }
  Serial.print("La valeur est : ");
  Serial.println(angle);
  }
}
```
