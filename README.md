# hexapodGUI
**HexapodGUI** is a Windows application (Written in C#) that **reads**, **writes** and **plots** data from/to serial port.

## Features
* Read and write data to serial ports even under high traffic load without freezing.
* Serial plotter for up to 5 different channels.
* Data logger to save incoming data to a **.txt** file.

## How to plot serial data?
In order for the data to be plotted, variables must be **seperated by comma ( , )** and a **newline ( \n )** character must be added at the end.

###Here an example code for [**Arduino**] platform
```arduino
#define setPoint  15.0    // Jarak robot dengan dinding
#define KP        0.1     // Konstanta Proporsional PID
#define KD        6.0     // Konstanta Derivative / Turunan PID
#define KI        1.1     // Konstanta Integral PID
#define TS        1       // Konstanta Time Sampling PID

float lastErr = 0;
float var1,
      var2,
      var3,
      var4,
      var5,
      var6,
      var7,
      var8,
      var9,
      var10;

void setup()
{
  Serial.begin(9600);
//  Serial.begin(19200);
//  Serial.begin(38400);
//  Serial.begin(57600);
//  Serial.begin(74880);
//  Serial.begin(115200);
}         

void loop()
{
  fullPID();
}

float PID(float pv)
{
  float err, P, D, I;

  err = setPoint - pv;
  P = KP * err;
  D = ((KD * 10.0) / TS) * (err - lastErr);
  I = ((KI / 10.0) * (err + lastErr)) * TS;

  lastErr = err;

  return (P + D + I);
}

void fullPID()
{
  float pv, dPID;
        pv   =   var7;
        PID(pv);
        dPID = PID(pv);

    var1 =   setPoint;
    var2 =   KP + 2.11;                       //Kp
    var3 =   KD;                              //Kd
    var4 =   KI;                              //Ki
    var5 =   PID(pv) + random(16.55, 17.55);  //PID
    var6 =   random(70, 75);                  //FPing
    var7 =   random(24, 26);                  //FLPing
    var8 =   random(45, 47);                  //FRPing
    var9 =   random(19, 20) + dPID;           //LRange
    var10 =  random(19, 20) - dPID;           //RRange
    
    //send variables
    Serial.print("HD");
    Serial.print(",");
    Serial.print(var1);
    Serial.print(",");
    Serial.print(var2);
    Serial.print(",");
    Serial.print(var3);
    Serial.print(",");
    Serial.print(var4);
    Serial.print(",");
    Serial.print(var5);
    Serial.print(",");
    Serial.print(var6);
    Serial.print(",");
    Serial.print(var7);
    Serial.print(",");
    Serial.print(var8);
    Serial.print(",");
    Serial.print(var9);
    Serial.print(",");
    Serial.print(var10);
    Serial.println();
    delay(200);
}
```
so data must be in this form
```
[Header],[setPoint],[Proportional],[Integral],[Derivative],[PID],[frontSensor],[leftBevelSensor],[rightBevelSensor],[leftRange],[rightRange]
```

