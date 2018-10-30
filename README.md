# b33rom3t3r
Pre party drinking game ! I bet you can beat my coluegue ( 1 red led),  green zone only for experts :)!


# # (CKECK OUT THE WIKI)




//Iniciem les variables Bglass i Reset que faràn la funció de reset i de cronòmetre

int BGLASS = 12;
int RESET = 13;

// Seguidament establirem un temps màxim per a un nombre de Led's, concretament 9 segons per 9 Led's,
// i utilitzarem les variables totalTime i currentTime per a sapiguer el temps total desde que el botó esta pulsat fins que es deixa de pulsar.

unsigned long MAXTIME = 9000;
unsigned long totalTime = 0;
unsigned long currentTime = 0;

// En el void setup indicarem el nombre de pins com a outputs, que aquets augmentaràn d'un en un, que es contarà a partir del pin 2 fins el pin 11 i  que tot això passarà quan el Pushbutton no estigui près.


void setup() {
  for (int i = 0; i < 9; i++) {
    pinMode(i + 2, OUTPUT);
    digitalWrite(i + 2, LOW);
  }
  //  Establirem les variables de l'inici Bglass i Reset com a inputs i generarem un ("Start!") per a començar amb el lloop.
  
  Serial.begin(9600);
  pinMode(BGLASS, INPUT);
  pinMode(RESET, INPUT);
  Serial.print("Start!");
  
}
// En el void loop, quan el input reset estigui près, els pins 10-2 passaràn a estar low ( i s'apagaran els leds corresponents amb una diferència de 0.03 s entre ells consecutivament)
//i seguidament els pins 10-2, també, passaràn a estar high, és a dir encesos amb la mateixa diferència.
//Finalment duguem a terme un ("reset"), establint el currenTime i el toTaltime a 0.


void loop() {

  if ( digitalRead(RESET) == LOW) {

    digitalWrite(10, LOW);
    delay (30);
    digitalWrite(9, LOW);
    delay (30);
    digitalWrite(8, LOW);
    delay (30);
    digitalWrite(7, LOW);
    delay (30);
    digitalWrite(6, LOW);
    delay (30);
    digitalWrite(5, LOW);
    delay (30);
    digitalWrite(4, LOW);
    delay (30);
    digitalWrite(3, LOW);
    delay (30);
    digitalWrite(2, LOW);
    delay (30);

    digitalWrite(10, HIGH);
    delay (30);
    digitalWrite(8, HIGH);
    delay (30);
    digitalWrite(7, HIGH);
    delay (30);
    digitalWrite(6, HIGH);
    delay (30);
    digitalWrite(5, HIGH);
    delay (30);
    digitalWrite(4, HIGH);
    delay (30);
    digitalWrite(3, HIGH);
    delay (30);
    digitalWrite(2, HIGH);
    delay (30);

    digitalWrite(10, LOW);
    delay (30);
    digitalWrite(9, LOW);
    delay (30);
    digitalWrite(8, LOW);
    delay (30);
    digitalWrite(7, LOW);
    delay (30);
    digitalWrite(6, LOW);
    delay (30);
    digitalWrite(5, LOW);
    delay (30);
    digitalWrite(4, LOW);
    delay (30);
    digitalWrite(3, LOW);
    delay (30);
    digitalWrite(2, LOW);
    delay (30);

    currentTime = 0;
    totalTime = 0;
    
    Serial.println("reset");
    //Si no està en marxa el ("reset") i el port BGLASS està près, establirem la variable currenTime a 0 i l'igualarem a millis. 
    //Si això no està pasant, comença a contar i a través de Serial.Print i Serial.printIn podem veure el temps que ha passsat i  un cop acaba, es torna  a establir el currentTime a 0.
    
    
  } else {
    if (digitalRead(BGLASS) == HIGH) {
      if (currentTime == 0) {
        currentTime = millis();
      }
    } else {
      if (currentTime > 0) {
        totalTime = totalTime + millis() - currentTime;
        currentTime = 0;
        Serial.print("Total time ");
        Serial.println(totalTime);
      }


    }

    // Serial.println((int)(getTime()/3000));
  }
  ledsOn();
}


//Per acabar introduim  el temps que transcurrirà entre led i led al encendres(1s.) quan BGLASS estigui près, sinò, els leds estaràn apagats ( si no es prem el ("reset")).


unsigned long getTime() {
  if (currentTime == 0) {
    return totalTime;
  } else {
    return totalTime + millis() - currentTime;
  }
}

//
void ledsOn() {

  int ledsOn = getTime() / 1000;

  //Serial.print(ledsOn);
  //Serial.println(" leds on");

  for (int i = 0; i < 9; i++) {
    if (i < ledsOn)
      digitalWrite(2 + i, HIGH);
    else
      digitalWrite(2 + i, LOW);
  }
}

