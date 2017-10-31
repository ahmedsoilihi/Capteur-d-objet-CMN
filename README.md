# Capteur-d-objet-CMN

![Capteur-d-objet-CMN](objet_fini.jpg)

## Présentation et objectifs
Etre capable de réaliser un projet au sein d'un FABLAB en présentant un système automatiser à partir d'un Arduino.<br> 
Comprendre un tas d'objet qui nous entoure, tous ces capteurs, pour au final en creer un.<br>

## Pré-requis
Savoir les bases de l'informatique.<br> 

### Matériel

Un Arduino	 6,65 EUR<br> 
Un câble USB	2,68 EUR<br>                                        
Un capteur de distance à ultrason	1,29 EUR<br> 
Une LED	0,10 EUR<br>
Les résistances	0,10 EUR<br>
Une Breadboard	2,36 EUR<br>    
Des fils de connexion	0,20 EUR<br>
Un adaptateur 5V	1,00 EUR<br>   

![Matériel](Elements.jpg)

### Logiciels
Cura pour l'imprimante 3D<br>
Fritzing pour les schéma connectique<br>

![Schéma](cura_1.PNG)
![Schéma](cura_2.PNG)
![Schéma](LED_RGB_US_Fritzing.png)

```c++
// Define pins for ultrasonic and ledpin
int const trigPin = 4;
int const echoPin = 2;
int const ledpin = 5;
void setup()
{Serial.begin(9600);
pinMode(trigPin, OUTPUT); // trig pin will have pulses output
pinMode(echoPin, INPUT); // echo pin should be input to get pulse width
pinMode(ledpin, OUTPUT); // led pin is output to control buzzering
}
void loop()
{
// Duration will be the input pulse width and distance will be the distance to the obstacle in centimeters
int duration, distance;
// Output pulse with 1ms width on trigPin
digitalWrite(trigPin, HIGH);
delay(1);
digitalWrite(trigPin, LOW);
// Measure the pulse input in echo pin
duration = pulseIn(echoPin, HIGH);
// Distance is half the duration devided by 29.1 (from datasheet)
distance = (duration/2) / 29.1;
      Serial.println(distance);// if distance less than 0.5 meter and more than 0 (0 or less means over range)
if (distance <= 5 && distance >= 0) {
// object detected
digitalWrite(ledpin, HIGH);
} else {
//no object
digitalWrite(ledpin, LOW);
}
// Waiting 60 ms 
delay(60);
}
```



## Capteur-d-objet-
Créer un détecteur de clef qui allumera une LED pour poser des objets métallique.<br> Le montage sera basé sur le capteur de distance à ultrason que l’on utilisera sous forme de seuil.<br> On partira donc du principe que le montage sera installé à un point fixe et que l’on détecte le passage devant le capteur.<br>
