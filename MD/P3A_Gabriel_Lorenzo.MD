# PRACTICA 3  : WIFI y BLUETOOTH

## A: GENERACIÓN DE UNA PÁGINA WEB

En esta práctica, deseamos realizar la conexión de nuestra placa ESP 32 a una wifi existente y posteriormente generar una página Web.

### Código

```cpp
#include <WiFi.h>
#include <WebServer.h>

// SSID & Password
const char* ssid = "VI-203-101-001-003";  // Enter your SSID here
const char* password = "Eo0Ep3ii";  //Enter your Password here

WebServer server(80);  // Object of WebServer(HTTP port, 80 is defult)

void handle_root(void);

void setup() {
 Serial.begin(115200);
 Serial.println("Try Connecting to ");
 Serial.println(ssid);

 // Connect to your wi-fi modem
 WiFi.begin(ssid, password);

 // Check wi-fi is connected to wi-fi network
 while (WiFi.status() != WL_CONNECTED) {
 delay(1000);
 Serial.print(".");
 }
 Serial.println("");
 Serial.println("WiFi connected successfully");
 Serial.print("Got IP: ");
 Serial.println(WiFi.localIP());  //Show ESP32 IP on serial

 server.on("/", handle_root);

 server.begin();
 Serial.println("HTTP server started");
 delay(100); 
}

void loop() {
 server.handleClient();
}

// HTML & CSS contents which display on web server
String HTML = "<!DOCTYPE html>\
<html>\
<body>\
<h1>My Página WEB con ESP32 &#128522;</h1>\
</body>\
</html>";

// Handle root url (/)
void handle_root() {
 server.send(200, "text/html", HTML);
}
```

### Funcionamiento del programa

En primer lugar, deberemos declarar dos librerías que son necesarias para nuestra práctica. En primer lugar, necesitamos la librería "WiFi.h" para conectar nuestra placa ESP32 a una red WiFi. En segundo lugar, también necesitamos la librería "WebServer.h" para generar un servidor web. Ahora vamos a declarar las variables globales que contienen el nombre y contrasña de la red wifi a la que nos vamos a conectar.

```cpp
#include <WiFi.h>
#include <WebServer.h>

// SSID & Password
const char* ssid = "VI-203-101-001-003";  // Enter your SSID here
const char* password = "Eo0Ep3ii";  //Enter your Password here

WebServer server(80);  // Object of WebServer(HTTP port, 80 is defult)

void handle_root(void);
```

Ahora encontramos la función Setup que tiene como objetivo inicar la conexión WiFi, una vez se haya relaizado nos lo mostrará por pantalla, posteriormente ejecuta la función "handle_root" y crea el servidor web en la IP indicada.

```cpp
void setup() {
 Serial.begin(115200);
 Serial.println("Try Connecting to ");
 Serial.println(ssid);

 // Connect to your wi-fi modem
 WiFi.begin(ssid, password);

 // Check wi-fi is connected to wi-fi network
 while (WiFi.status() != WL_CONNECTED) {
 delay(1000);
 Serial.print(".");
 }
 Serial.println("");
 Serial.println("WiFi connected successfully");
 Serial.print("Got IP: ");
 Serial.println(WiFi.localIP());  //Show ESP32 IP on serial

 server.on("/", handle_root);

 server.begin();
 Serial.println("HTTP server started");
 delay(100); 
}
```

Finalmente crearemos una variable tipo string donde guardaremos el texto que deseamos mostrar en el Servidor Web.

```cpp
// HTML & CSS contents which display on web server
String HTML = "<!DOCTYPE html>\
<html>\
<body>\
<h1>My Página WEB con ESP32 &#128522;</h1>\
</body>\
</html>";

// Handle root url (/)
void handle_root() {
 server.send(200, "text/html", HTML);
}
```

### Salida por el Terminal

![](IMG3.png)

