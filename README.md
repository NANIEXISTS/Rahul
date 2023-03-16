int t1_out = 10;
int f1_in = 8;
float f1;
int f1_1;
float f1_read;
int f2_in = 9;
float f2;
int f2_1;
float f2_read;
int potPin = 4;
int ERROR_LED = 2;
float potval;
float cal_val =0;
float a1 = 0;
float a2 = 0;
float a3 = 0;
float a4 = 0;
float ana_avg;
float half_max;
int f1_1;
int f2_1;
Ticker ticker;


void setup() {
  // put your setup code here, to run once:
  Serial.begin(9600);
  pinMode(t1_out, OUTPUT);
  pinMode(f1_in, INPUT);
  pinMode(f2_in, INPUT);
  pinMode(potPin, INPUT);
  pinMode(ERROR_LED, OUTPUT);
  

}

void loop() {
  // put your main code here, to run repeatedly:

}

void task1()
{
  

  digitalWrite(led, HIGH);
  delayMicroseconds(200);
  digitalWrite(led, LOW);
  delayMicroseconds(50);
  digitalWrite(led, HIGH);
  delayMicroseconds(30);  
  digitalWrite(led, LOW);
  
}


void task2()
{
  f1_read = pulseIn(f1_in, HIGH);
  f1 = 1000000 / (f1_read);
}

void task3()
{
  f2_read = pulseIn(f2_in, HIGH);
  f2 = 1000000 / (f2_read);
}


void task4()
{
  potval = analogRead(potPin);
  cal_val = (3.3*potval)/4095;
  a1 = a2;
  a2 = a3;
  a3 = a4;
  a4 = cal_val;
  ana_avg = (a1 + a2 + a3 + a4)/4;
  half_max = 3.3/2;
  if (ana_avg > half_max)  {digitalWrite(ERROR_LED, HIGH);}
  else {digitalWrite(ERROR_LED, LOW);}
}


void task_5()
{
  f1_1 = 0;
  f2_1 = 0;
  f1_1 = ((f1 - 333)*99)/(1000 - 333);
  f2_1 = ((f2 - 500)*99)/(1000 - 500);
  Serial.printf("%d, %d\n",f1_1, f2_1);
}

