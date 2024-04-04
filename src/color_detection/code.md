# Farberkennung
Hier ist der Code für die Farberkennung:
```c
#define S0  26
#define S1  25
#define S2  14
#define S3  27
#define OUT 13

#define R_LED 12
#define G_LED 33
#define B_LED 32

int r = 0;
int g = 0;
int b = 0;

void setup() {
  pinMode(S0, OUTPUT);
  pinMode(S1, OUTPUT);
  pinMode(S2, OUTPUT);
  pinMode(S3, OUTPUT);
  pinMode(OUT, INPUT);

  pinMode(R_LED, OUTPUT);
  pinMode(G_LED, OUTPUT);
  pinMode(B_LED, OUTPUT);

  digitalWrite(S0, HIGH);
  digitalWrite(S1, LOW);

  Serial.begin(9600);
}

void loop() {
  digitalWrite(S2, LOW);
  digitalWrite(S3, LOW);

  r = map(pulseIn(OUT, LOW), 25, 70, 255, 0);
  Serial.print("R= "); Serial.print(r); Serial.print("   ");
  delay(100);

  digitalWrite(S2, HIGH);
  digitalWrite(S3, HIGH);

  g = map(pulseIn(OUT, LOW), 25, 70, 255, 0);
  Serial.print("G= "); Serial.print(g); Serial.print("   ");
  delay(100);

  digitalWrite(S2, LOW);
  digitalWrite(S3, HIGH);

  b = map(pulseIn(OUT, LOW), 25, 70, 255, 0);
  Serial.print("B= "); Serial.print(b); Serial.println("   ");
  delay(100);

  if (r > 100 && r > g && r > b) {
    digitalWrite(R_LED, HIGH);
    digitalWrite(G_LED, LOW);
    digitalWrite(B_LED, LOW);
  } else if (g > 100 && g > r && g > b) {
    digitalWrite(R_LED, LOW);
    digitalWrite(G_LED, HIGH);
    digitalWrite(B_LED, LOW);
  } else if (b > 100 && b > r && b > g) {
    digitalWrite(R_LED, LOW);
    digitalWrite(G_LED, LOW);
    digitalWrite(B_LED, HIGH);
  } else {
    digitalWrite(R_LED, LOW);
    digitalWrite(G_LED, LOW);
    digitalWrite(B_LED, LOW);
  }
}
```