```.ino
// define pins
int buzzer = 13;
int bottom_row = 12;
int top1 = 5;
int top2 = 6;
int top3 = 7;
int top4 = 8;
int top5 = 9;
int top6 = 10;
int top7 = 11;

// buzzer output for morse code dot
void dot(){
  tone(buzzer, 1000);
  delay(200);
  noTone(buzzer);
  delay(500);
}

// buzzer output for morse code dash
void dash(){
  tone(buzzer, 1000);
  delay(600);
  noTone(buzzer);
  delay(500);
}

void out0(){
  delay(300);
  digitalWrite(top1, HIGH);
  digitalWrite(top2, HIGH);
  digitalWrite(top3, HIGH);
  digitalWrite(top4, HIGH);
  digitalWrite(top5, HIGH);
  digitalWrite(top6, HIGH);
  digitalWrite(top7, HIGH);
  digitalWrite(bottom_row, HIGH);
  dash();
  dash();
  dash();
  dash();
  dash();
  digitalWrite(top1, LOW);
  digitalWrite(top2, LOW);
  digitalWrite(top3, LOW);
  digitalWrite(top4, LOW);
  digitalWrite(top5, LOW);
  digitalWrite(top6, LOW);
  digitalWrite(top7, LOW);
  digitalWrite(bottom_row, LOW);
}

void out1(){
  delay(300);
  digitalWrite(top4, HIGH);
  dot();
  dash();
  dash();
  dash();
  dash();
  digitalWrite(top4, LOW);
}

void out2(){
  delay(300);
  digitalWrite(top3, HIGH);
  digitalWrite(top5, HIGH);
  dot();
  dot();
  dash();
  dash();
  dash();
  digitalWrite(top3, LOW);
  digitalWrite(top5, LOW);
}

void out3(){
  delay(300);
  digitalWrite(top2, HIGH);
  digitalWrite(top4, HIGH);
  digitalWrite(top6, HIGH);
  dot();
  dot();
  dot();
  dash();
  dash();
  digitalWrite(top2, LOW);
  digitalWrite(top4, LOW);
  digitalWrite(top6, LOW);
}

void out4(){
  delay(300);
  digitalWrite(top1, HIGH);
  digitalWrite(top3, HIGH);
  digitalWrite(top5, HIGH);
  digitalWrite(top7, HIGH);
  dot();
  dot();
  dot();
  dot();
  dash();
  digitalWrite(top1, LOW);
  digitalWrite(top3, LOW);
  digitalWrite(top5, LOW);
  digitalWrite(top7, LOW);
}

void out5(){
  delay(300);
  digitalWrite(bottom_row, HIGH);
  dot();
  dot();
  dot();
  dot();
  dot();
  digitalWrite(bottom_row, LOW);
}

void out6(){
  delay(300);
  digitalWrite(top4, HIGH);
  digitalWrite(bottom_row, HIGH);
  dash();
  dot();
  dot();
  dot();
  dot();
  digitalWrite(top4, LOW);
  digitalWrite(bottom_row, LOW);
}

void out7(){
  delay(300);
  digitalWrite(top3, HIGH);
  digitalWrite(top5, HIGH);
  digitalWrite(bottom_row, HIGH);
  dash();
  dash();
  dot();
  dot();
  dot();
  digitalWrite(top3, LOW);
  digitalWrite(top5, LOW);
  digitalWrite(bottom_row, LOW);
}

void out8(){
  delay(300);
  digitalWrite(top2, HIGH);
  digitalWrite(top4, HIGH);
  digitalWrite(top6, HIGH);
  digitalWrite(bottom_row, HIGH);
  dash();
  dash();
  dash();
  dot();
  dot();
  digitalWrite(top2, LOW);
  digitalWrite(top4, LOW);
  digitalWrite(top6, LOW);
  digitalWrite(bottom_row, LOW);
}

void out9(){
  delay(300);
  digitalWrite(top1, HIGH);
  digitalWrite(top3, HIGH);
  digitalWrite(top5, HIGH);
  digitalWrite(top7, HIGH);
  digitalWrite(bottom_row, HIGH);
  dash();
  dash();
  dash();
  dash();
  dot();
  digitalWrite(top1, LOW);
  digitalWrite(top3, LOW);
  digitalWrite(top5, LOW);
  digitalWrite(top7, LOW);
  digitalWrite(bottom_row, LOW);
}

void setup()
{
  Serial.begin(9600);
  // introduction sequence
  Serial.print("This program converts roman numerals to mayan numerals and morse code\n");
  Serial.print("Input either a single digit number, or count using the following format: count, start, end, up or down\n");
  Serial.print("Example of counting: count, 1, 9, up will count from 1 to 9\n");
}

// store input in buffer
const int buffer_size = 50;
char buffer[buffer_size];

void loop(){
  char input;
  int number;
  // take user input
  Serial.print("Enter input: \n");
  while (Serial.available() == 0){
  }
  input = Serial.readBytes(buffer, buffer_size);
  
  // check if single conversion or counting
  if (strlen(buffer) == 1){ // if length of user input is 1 (input is a 1 digit number), enable single conversion
    number = atoi(buffer);
  }
    
  // single conversion
  if (number == 0){
    out0();
  }
  if (number == 1){
    out1();
  }
  if (number == 2){
    out2();
  }
  if (number == 3){
    out3();
  }
  if (number == 4){
    out4();
  }
  if (number == 5){
    out5();
  }
  if (number == 6){
    out6();
  }
  if (number == 7){
    out7();
  }
  if (number == 8){
    out8();
  }
  if (number == 9){
    out9();
  }
  
  // check if counting
  char *check;
  char *if_up;
  char *if_down;
  int start = buffer[7] - 48;
  int end = buffer[10] - 48;
  check = strstr(buffer, "count"); // check if "count" is in user input
  if_up = strstr(buffer, "up"); // check if "up" is in user input
  if_down = strstr(buffer, "down"); // check if "down" is in user input
  if (check){ // if "count" is in user input
    if (if_up){ // if counting upwards
      for (start; start < end + 1; start++){
        if (start == 0){
          out0();
        }
        if (start == 1){
          out1();
        }
        if (start == 2){
          out2();
        }
        if (start == 3){
          out3();
        }
        if (start == 4){
          out4();
        }
        if (start == 5){
          out5();
        }
        if (start == 6){
          out6();
        }
        if (start == 7){
          out7();
        }
        if (start == 8){
          out8();
        }
        if (start == 9){
          out9();
        }
      }
    }
    if (if_down){ // if counting downwards
      for (start; start > end - 1; start--){
        if (start == 0){
          out0();
        }
        if (start == 1){
          out1();
        }
        if (start == 2){
          out2();
        }
        if (start == 3){
          out3();
        }
        if (start == 4){
          out4();
        }
        if (start == 5){
          out5();
        }
        if (start == 6){
          out6();
        }
        if (start == 7){
          out7();
        }
        if (start == 8){
          out8();
        }
        if (start == 9){
          out9();
        }
      }
    }
  }
  
}
```
