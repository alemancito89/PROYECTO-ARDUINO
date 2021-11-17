//Libraries
#include <DHT.h>;
//I2C LCD:
#include <LiquidCrystal_I2C.h>
#include <Wire.h>

LiquidCrystal_I2C lcd(0x27,16,2); //establezca la dirección LCD en 0x27 para una pantalla de 16 caracteres y 2 líneas
  
//Constantes
#define DHTPIN 7     // a que pin estamos conectados
#define DHTTYPE DHT11   // DHT 11
DHT dht(DHTPIN, DHTTYPE); //// Inicializar el sensor DHT para Arduino normal de 16 mhz

//Variables
//int chk;
int h;  //Almacena el valor de la humedad
int t; //Almacena el valor de la temperatura
void setup()
{
    Serial.begin(9600);
    Serial.println(" Prueba de sensor de temperatura y humedad");
    dht.begin();
    lcd.init(); //inicializar la pantalla lcd
    lcd.backlight(); //abre la luz de fondo
}

void loop()
{
    //Leer datos y almacenarlos en variables h (humedad) y temperatura)
    // La lectura de temperatura o humedad tarda 250 milisegundos
    h = dht.readHumidity();
    t = dht.readTemperature();
    
   // Imprime los valores de temperatura y humedad en el monitor en serie
    Serial.print("HUMEDAD: ");
    Serial.print(h);
    Serial.print(" %, TEMP: ");
    Serial.print(t);
    Serial.println(" ° CELCIUS");
        
// coloca el cursor en (0,0):
// imprimir de 0 a 9:
    lcd.setCursor(0, 0);
    lcd.println(" TEMP. JOSE A.M ");
    
    lcd.setCursor(0, 1);
    lcd.print("T:");
    lcd.print(t);
    lcd.print("C");

    lcd.setCursor(6, 1);
    lcd.println("2021 ");
     
    lcd.setCursor(11, 1);
    lcd.print("H:");
    lcd.print(h);
    lcd.print("%");
    
  delay(1000); //Retraso 1 seg.
}
