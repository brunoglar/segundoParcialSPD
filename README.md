# **<span style="color:white">Examen práctico domiciliario de SPD👨‍💻**

---

![Arduino](https://d1e4pidl3fu268.cloudfront.net/1e27d448-be48-4a6a-97e9-855e2321ad37/images.crop_222x168_38,0.preview.png)

## **<span style="color:yellow">Integrantes:**

---

- ### <span style="color:white">**Bruno Gaston Luna**

## **<span style="color:yellow">Proyecto: Sistema de Incendio con Arduino**

---

![Tinkercad](segundoParcialSpd "Vista previa, esquema en Tinkercad")

## **<span style="color:yellow">Consigna del Sistema de Incendio:**

---

<span style="color:white">El objetivo de este proyecto es diseñar un **sistema de incendio** utilizando Arduino que pueda
detectar cambios de temperatura y activar un servo motor en caso de detectar un incendio.
Además, se mostrará la temperatura actual y la estación del año en un display LCD.

---

## **<span style="color:yellow">Función principal**

<span style="color:white">La **funcionalidad principal** del programa, es actuar como un sistema
de incendios. Si la temperatura ambiente está por debajo de los **<span style="color:green">60°**, se considera un **rango aceptable** y el sistema mostrará la temperatura ambiente, con su estación del año correspondiente y el led verde indicará que el sistema está encendido y en óptimas condiciones, si la temperatura está en el rango (**<span style="color:yellow">60° - 90°**) el display lanzará una advertencia de que hay
alguna anomalía en el sistema, con el encendido del led amarillo intermitente. Si la temperatura excede los **<span style="color:red">90°** actuará el modo emergencia del sistema activando así también la funcionalidad del servomotor encendiendo también el led rojo intermitente a modo de emergencia.

> **<span style="color:green">#include <IRremote.h>
#include <LiquidCrystal.h>
#include <Servo.h>**

<span style="color:white">Son **librerías** que utilizamos para llamar a las clases y crear los objetos para el correcto funcionamiento del programa.  continuación una breve parte del código. Si desea ver el código completo en su totalidad, acceda mediante el link brindado al final del proyecto.

# 👨‍💻

```
#include <IRremote.h>
#include <LiquidCrystal.h>
#include <Servo.h>


#define botonEncendido 4278238976
#define ledVerde 13
#define ledRojo 12
#define ledAmarillo 8
#define sensorTemp A0
int recI = 11;

LiquidCrystal lcd (2,3,4,5,6,7);
Servo servoIncendio;
IRrecv irrecv(recI);
decode_results results;

void setup()
{
  pinMode(ledRojo, OUTPUT);
  pinMode(ledVerde, OUTPUT);
  pinMode(ledAmarillo, OUTPUT);
  servoIncendio.attach(9);
  lcd.begin(16,2);
  Serial.begin(9600);
  irrecv.enableIRIn();
}

int estado = 0;
int tempAmbiente = 0;
int lectura = 0;
int inicioAng = 0;
int finalAng = 180;
int incremento = 30;
unsigned long captor = 0; /


void loop() {


  if (irrecv.decode(&results)) {

    if (IrReceiver.decode()) {
    	Serial.println(IrReceiver.decodedIRData.decodedRawData);
    	captor = IrReceiver.decodedIRData.decodedRawData;
	}

    if (captor == botonEncendido){
    	estado = !estado;
    }

    irrecv.resume();
  }

  if(estado == 1){

    tempAmbiente = lecturaSensor(sensorTemp);
    Serial.println(tempAmbiente);
    digitalWrite(ledRojo, 0);


```

# 🤖 _<span style="color:white">ENLACES A GDB Y TINKERCAD_

> Apreta en el link para acceder al código en  [GDB](https://onlinegdb.com/1RDcLsX0C)

> **Apreta en el link para acceder al proyecto y visualizar su funcionamiento en
> [TinkerCad](https://www.tinkercad.com/things/fPKjwBBHPyg-segundo-parcial-de-spd-bruno-g-luna-division-1g/editel?sharecode=XQruo-gjm2owohkvtMYp6jzrHs--W358zOo1vOviUhc)**
