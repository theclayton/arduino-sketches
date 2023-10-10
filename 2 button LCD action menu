/*
2 button LCD action menu

Shows a splash screen with instructions.
Then dispalys a list of actions, such as turn an LED on, or run a servo motor.

Left button scrolls through menu, right selects an item.
*/

#include <LiquidCrystal.h>
#include <Servo.h>

const int rs = 13, en = 12, d4 = 11, d5 = 10, d6 = 9, d7 = 8;
LiquidCrystal lcd(rs, en, d4, d5, d6, d7);

const int leftButtonPin = 3;
const int rightButtonPin = 5;

int index = 0;
String menuArr[4] = {"Do nothing    ", "Turn on LED   ", "Run Servo     "}; 

bool rightPressed = false;
bool leftPressed = false;

Servo theServo;
int servoPos = 0;

// Custom LCD characters
byte rightArrow[8] = {
  B00000,
  B01000,
  B01100,
  B01110,
  B01100,
  B01000,
  B00000,
};

void setup() {
  // Setup custom lcd characters
  lcd.createChar(0, rightArrow);

  // Connected items
  pinMode(LED_BUILTIN, OUTPUT);
  theServo.attach(6);

  // Setup the LCD"s number of columns and rows:
  lcd.begin(16, 2); 
  lcd.clear();

  // Welcome splash screen
  lcd.setCursor(0, 0);
  lcd.print("Welcome to");
  lcd.setCursor(0, 1);
  lcd.print("the LCD menu!");

  delay(3000);
  lcd.clear();

  lcd.setCursor(0, 0);
  lcd.print("Select an item");
  lcd.setCursor(0, 1);
  lcd.print("the following:");

  delay(3000);
  lcd.clear();
  // End splash screen

  // Display first 2 items in menu
  lcd.setCursor(0, 0);
  lcd.write(byte(0));
  lcd.print(" " + menuArr[0]);
  lcd.setCursor(0, 1);
  lcd.print("  " + menuArr[1]);

  // Serial bps rate for debugging
  // Serial.begin(9600);
}

void loop() {
  if (leftPressed == false && digitalRead(leftButtonPin) == HIGH) {
    leftPressed = true;
    handleLeftPress();
  } else if (leftPressed == true && digitalRead(leftButtonPin) == LOW) {
    leftPressed = false;
  }

  if (rightPressed == false && digitalRead(rightButtonPin) == HIGH) {
    rightPressed = true;
    handleRightPress();
  } else if (rightPressed == true && digitalRead(rightButtonPin) == LOW) {
    rightPressed = false;
  };
}

// Move index down menu
void handleLeftPress() {
  if (index >= 2) { // or arr length
    index = 0;
  } else {
    index++;
  }

  lcd.setCursor(0, 0);
  lcd.write(byte(0));
  lcd.print(" " + menuArr[index]);

  if (index == 2) { // second to last item
    lcd.setCursor(0, 1);
    lcd.print("  " + menuArr[0]);
  } else {
    lcd.setCursor(0, 1);
    lcd.print("  " + menuArr[index + 1]);
  }
}

// Perform action at menu index that is currently selected
void handleRightPress() {
  if (index == 1) {
    if (digitalRead(LED_BUILTIN) == LOW) {
      digitalWrite(LED_BUILTIN, HIGH);
    } else {
      digitalWrite(LED_BUILTIN, LOW);
    }
  } else if (index == 2) {
    if (servoPos > 90) {
      theServo.write(10);
    } else {
      theServo.write(180);
    }
  }
}
