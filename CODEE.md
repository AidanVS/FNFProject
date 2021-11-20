int bands = 512;

float radius = 1000;
int x = 540;
int y = 400;
float speed = 12;
int count = -45;
int keys = UP;
int score = 1;
PImage img;
PImage bg;
boolean press = false;
int combo = 0;
String status = "";
boolean hit = false;
int y2= y;

int r = 0;
int g = 0;
int b = 0;
PImage Up;
PImage Right;
PImage Down;
PImage Left;
PImage Up_S;
PImage Right_S;
PImage Down_S;
PImage Left_S;

void setup(){
  frameRate(60);
  size(1462, 712);
  bg = loadImage("sanic.png");
  Up = loadImage("Up_Empty.png");
  Right = loadImage("Right_Empty.png");
  Down = loadImage("Down_Empty.png");
  Left = loadImage("Left_Empty.png");
  Up_S = loadImage("Up_Solid.png");
  Right_S = loadImage("Right_Solid.png");
  Down_S = loadImage("Down_Solid.png");
  Left_S = loadImage("Left_Solid.png");


}
void draw(){
   keyReleased();
   background(bg);
   
   
   //prints the hitbox of the arrows
   tint(0,0,0,100);
   imageMode(CENTER);




   imageMode(CORNER);
   tint(255);
   
   //spawns an arrow when the last one dissapears
   if (count == 46 || count == -45){
     count = 0;
     //decides what arrow to ouput
     spawnRect(random(0,4));
   }
   //checks if keys are correctly hit
   move();
   textSize(50);
   stroke(255);
   text("COMBO: " + combo,850,100);
   fill(r,g,b);
   textSize(40);
   textAlign(CENTER);
   //hit or miss status
   text(status,100,y2 + 110);
}

void spawnRect(float i){
  if( i >= 0 && i < 1){
    keys = UP;
    img = loadImage("Up.png");
    y = 600;
  }
  if( i >= 1 && i < 2){
    keys = RIGHT;
    img = loadImage("Right.png");
    y = 400;
  }
  if( i >= 2 && i < 3){
     keys = DOWN;
     img = loadImage("Down.png");
     y = 200;
  }
  if( i >= 3 && i <= 4){
    keys = LEFT;
    img = loadImage("Left.png");
    y = 0;
  }
}

void move(){
  if (keyPressed) {
    if (keyCode == keys && x < 50 && press == false) {
      score += 100 * combo;
      combo++;
      press = true;
      hit = true;
      status = "SICK";
      y2 = y;
      r = 0;
      g = 255;
      b = 255;
    }
    if (keyCode == keys && x < 100 && x >= 50 && press == false) {
      score += 50 * combo;
      combo++;
      press = true;
      hit = true;
      status = "GOOD";
      y2 = y;
      r = 0;
      g = 255;
      b = 0;
    }
    if (keyCode == keys && x > 100 && press == false){
      combo = 1;
      status = "MISS";
      y2 = y;
      r = 255;
      g = 0;
      b = 0;
    }
    if (keyCode != keys && x > 100 && x < 450){
      combo = 1;
      status = "MISS";
      y2 = y;
      r = 255;
      g = 0;
      b = 0;
    }
  }
  if (hit != true && x == 0){
      combo = 1;
      status = "MISS";
      y2 = y;
      r = 255;
      g = 0;
      b = 0;
    }
  fill(255);
  image(img,x,y,200,200);
  x -= 1*speed;
  count++;
  if(x < 0){
    x = 540;
    hit = false;
  }
}

//so you cant hold down keys
void keyReleased(){
  if (!keyPressed){
    press = false;
  }
}

//prints using the colors I want in the correct location
void printRects(int y,int r, int b, int g, PImage img, int _X, int _Y){
   stroke(r,g,b,100);
   fill(r,g,b,50);
   rect(0,y,200,200);
   rect(0,y,600,200);
   line(200,y + 50,600,y + 50); 
   line(200,y + 100,600,y + 100); 
   line(200,y + 150,600,y + 150); 
   fill(r,g,b,50);
   tint(r,g,b, 100);
   imageMode(CENTER);
}
