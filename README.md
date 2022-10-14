# Verkefnalýsing

Strax í upphafi fundum við rör sem hæfðu hugmyndinni okkar, síðan teiknuðum við litla skýringarmynd af verkefninu, svo í næstu kennslustund fórum við að útfæra það

![https://github.com/NITEOFF/Verkefni5Vesm1/blob/main/Mappa/Lysing.jpg](https://github.com/NITEOFF/Verkefni5Vesm1/blob/main/Mappa/Lysing.jpg)

Í fyrsta lagi var kjálkaverkið þróað, eftir vel heppnaða sjósetningu var haldið áfram í næsta verkefni, (Samhliða þessu reyndi Triggvi að ná góðum snúningi hja bakinu)

![https://github.com/NITEOFF/Verkefni5Vesm1/blob/main/Mappa/hausinni.jpg](https://github.com/NITEOFF/Verkefni5Vesm1/blob/main/Mappa/hausinni.jpg)

Svo fórum við að hljóma með hann, fyrstu vandamálin komu upp, þar sem ekki var hægt að tengja báða hátalarana venjulega, það komu alltaf einhverjar villur, í kjölfarið var vandamálið líka leyst (Hér fyrir neðan má hlusta á hljóðið sjálft með því að smella á myndina hér að neðan)

[![Hlusta](https://github.com/NITEOFF/Verkefni5Vesm1/blob/main/Mappa/skeletonhead.jpg)](https://youtu.be/cod4-cErUxs)

# Kóðinn
  ## NOTE: vegna vandamala vildi foritid ekki virka eins og ati <br />
  #include "Arduino.h" <br />
  #include "SoftwareSerial.h" <br />
  #include "DFRobotDFPlayerMini.h" <br />
  #include <Servo.h> <br />

  Servo myservo_jaw;   // Kjalki
  Servo myservo_neck;  // hals

  // Sound
  
    SoftwareSerial mySoftwareSerial(10, 11);  // assignes the sound card to (pin 10 and 11)
    DFRobotDFPlayerMini myDFPlayer;

  //back movement
  
    int enA = 9; // Motor controle
    int in1 = 8; // motor pin 1
    int in2 = 7; // motor pin 2

  //jaw movement
  
    int jawPin = 5; // assignees the data cable to plug 5
    int jawPos = 90; sets the degree to 90

  // NECK movement
  
    int neckPin = 3; // assignees the data cable to plug 3
    int neckPos = 90;

  //eyes
  
    int eyePinR = 12; // assignees the data cable to plug 12 <br />
    int eyePinL = 13; // assignees the data cable to plug 13 <br />
    bool eyePowerR = 1; // controles the Right eye ON - OFF <br />
    bool eyePowerL = 1; // controles the Left eye ON - OFF <br />


  void setup() {
  
    // Set all the motor control pins to outputs <br />
    pinMode(enA, OUTPUT); <br />
    pinMode(in1, OUTPUT); <br />
    pinMode(in2, OUTPUT); <br />
    pinMode(eyePinL, OUTPUT); <br />
    pinMode(eyePinR, OUTPUT); <br />
    digitalWrite(eyePinL, eyePowerL); <br />
    digitalWrite(eyePinR, eyePowerR); <br />


  // Sound setup 
  
    mySoftwareSerial.begin(9600);  // notum softwareSerial í samskiptum við mp3.
    if (!myDFPlayer.begin(mySoftwareSerial)) {
    while(true);
    }

  }

  void loop() {
  
    //bodyMotorPower();
    //jawMovement();
    //neckMovement();
  }

  // // This function lets you control the main motor
  void bodyMotorPower() {

    analogWrite(enA, 220);  // MotorPower. 0 - 255

    // Turn on pin 1
    digitalWrite(in1, HIGH);
    digitalWrite(in2, LOW);
    delay(300);

    // Turn off motor
    digitalWrite(in1, LOW);
    digitalWrite(in2, LOW);
    delay(1000);

    // Now change motor directions
    digitalWrite(in1, LOW);
    digitalWrite(in2, HIGH);
    delay(300);

    // Turn off motor
    digitalWrite(in1, LOW);
    digitalWrite(in2, LOW);
    delay(1000);
  }

  void playSound() {
  
    Servo myservo;
    int pos = 0;
    myDFPlayer.volume(30);  // Hljóðstyrkur (volume) frá 0 til 30  (má líka vera í setup)
    myDFPlayer.play(1);     // spilum fyrsta mp3 á SD kortinu.
    for (pos = 0; pos <= 60; pos += 1) {
      myservo.write(pos);
      delay(5);
    }
    for (pos = 60; pos >= 50; pos -= 1) {
      myservo.write(pos);
      delay(5);
    }
  }

  void jawMovement() {

     myDFPlayer.volume(0);  // Hljóðstyrkur (volume) frá 0 til 30  (má líka vera í setup)
     myDFPlayer.play(1);     // spilum fyrsta mp3 á SD kortinu.
     delay(1000);            // leyfum hljóðskrá að klárast, tekur 4 sekúndur. 

    myservo_jaw.attach(jawPin);
    myservo_neck.attach(neckPin);

    for (int i = 0; i < 110; i += 2) {
      myservo_jaw.write(i);
      delay(20);
    }
    delay(500);
  }

  void neckMovement() {
  
    for (int i = 0; i < 90; i += 2) {  // goes from 0 degrees to 180 degrees
      // in steps of 1 degree
      myservo_neck.write(i);  // tell servo to go to position in variable 'pos'
      delay(50);              // waits 15 ms for the servo to reach the position
    }
    delay(500);

  }

Hópur - Artjom Pushkar, Tryggvi Þór Bogason, Sölvi Hrafn Pétursson
