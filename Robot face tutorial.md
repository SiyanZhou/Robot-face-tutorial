# Use Processing to Bulid an Talking Robot Face

###### By Siyan Zhou 7/24/2017

This tutorial introduces how to use Processing to bulid an animated and interactive talking robot face on your computer screen. It also covers some computer programing basics along the way. I assumed you already have Processing installed on your computer. If not, you can read the [tutorial by Casey Reas and Ben Fry](https://processing.org/tutorials/gettingstarted/) to get started.

## Coodinate System
Before we begin programming with Processing, we must understanding that  computer screen is nothing more than a fancier piece of graph paper. Each pixel of the screen is a coordinate - two numbers, an "x" (horizontal) and a "y" (vertical) - that determines the location of a point in space. Similar to Cartesian coordinate system you leanred in eighth grade, (0,0) can be found at the top left with both positive x-axis pointing to the right and positive y-axis pointing down. And it is our job to specify what shapes and colors should appear at these pixel coordinates.
 
 
![coordinate system](http://py.processing.org/tutorials/drawing/imgs/1.3.jpg)  

But before you can draw anything on the screen, you need to tell the comupter the size of a window, where you can define coordinates. You can type the size fuction in the processing editor. A function is the instruction you want the computer to follow and it is wrritten in a way a computer can read. Here, an size function example will look like this: 
          
```java
size(1120,630);
```
 
If you run this code in the processing editor, a empty display window with 1120 pixels in width and 630 pixels in height will appear on the screen:

![display window](pictures/display window.png)




## Simple Shapes
As you can see the robot face example at the begining of the tutorial, we need to at least intruct the computer to draw a big rectangular for the face outline, three arcs for the eyelids and lips, and then four ellipses for the eyes. Some shape functions will look like this:

![rect](https://processing.org/reference/images/rect_1.png)

```java
rect(x, y, width, height, radii);
```

* "x" is the x-coordinate for the top left corner of the rectangle
* "y" is the y-coordinate for the top left corner of the rectangle
* "width" is the width of the rectangle
* "height" is the height of the rectangle
* "radii" the radii for all four corners 


![arc](https://processing.org/reference/images/arc_3.png)
	
```java
arc(x, y, width, height, start, stop);
```
	
      
* "x" is the x-coordinate for the centerpoint of the arc's ellipse
* "y" is the y-coordinate for the centerpoint of the arc's ellipse
* "width" is the width of the arc's ellipse
* "height" is the height of the arc's ellipse
* "start" is the angle to start the arc, specified in radians
* "stop" is the  angle to stop the arc, specified in radians

![ellipse](https://processing.org/reference/images/ellipse_.png)

```java
ellipse(x, y, width, height);
```


* "x" is the x-coordinate for the centerpoint of the ellipse
* "y" is the y-coordinaten for the centerpoint of the ellipse
* "width" is the width of the ellipse
* "height" is the height of the ellipse

## Color

In the digital world, color is defined as a range of numbers. In our robot face example we only need to discuss about the simplest case: black & white or grayscale. 0 means black, 255 means white. In between, every other number—50, 87, 162, 209, and so on—is a shade of gray ranging from black to white.

![color](https://processing.org/tutorials/color/imgs/grayscale.svg)

By adding the `stroke()` and `fill()` functions before something is drawn, we can set the color of any given shape. There is also the function background(), which sets a background color for the window. Here are example codes to draw the robot face(anyting wrritten after `//` in a line is a comment):
 
 ```java
size(1120,630);                       //set the size of the window
background(190);                      //Set the background to gray

stroke(0);                            //Set the stroke to black                
strokeWeight(5);                      //Set the thickness of the stroke  
fill(255);                            //Set the interior the following shape to white
rect(210, 70, 700, 420, 70);          //draw the face outline

strokeWeight(5);                      
arc(385, 210, 210, 140, PI, 2*PI);    //draw the right eyelid 
arc(735, 210, 210, 140, PI, 2*PI);    //draw the left eyelid

fill(0);                              //Set the interior the following shape to white
ellipse(385,210,70,140);              //draw the right big eyeball
ellipse(735,210,70,140);              //draw the left big eyeball

fill(255);
ellipse(385,210,17.5,17.5);           //draw the right small eyeball
ellipse(735,210,17.5,17.5);           //draw the left small eyeball


fill(255);                            
stroke(0);
strokeWeight(5);
arc(560,371,140,70,0 ,PI);            //draw the mouth
 ```
 
 &nbsp;
 
 ![static robot face](pictures/static robot face.png)
 
## Flow(setup and draw)
Even though we are able to tell the computer to draw a robot face with simple shapes and colors, they are all static images on the screen. In order to make an animated face, we need to understand the concept of the control flow. As you can see in the code example for the robot face above, each line of code is generally executed from top to bottom. Control flow structures, however, can allow you change execution order and determine what section of code is run in a program at a given time. You can regulate the flow of your program's execution with control statements and loops. Here is an example of such control flow statement: 

```java
void setup(){
//any line of code within these curly brackets only happen once
}

void draw(){
//any line of code within these curly brackets is executed repeatively and continuously each frame until the program is stopped
}

```
## Variables
One of the interactive features is that the robot's eyes track the mouse movement, so we need to vary the eyes's location according to the mouse postion. We need some mechanism for dynamically storing the mouse's location - variables.

### Built-in varibles
`mouseX ` and `mouseY` are built-in varibles in Processing. There are variables that stand for the X and Y location of the mouse. `width` and `height` are also Processing built-in variables which store the the current value for the width and height of the window. Built-in variable `frameCount` contains the number of frames that have been displayed since the program started. All these variables, which Procceing know what it is almost magically, were of cource implemented by some other programmers when Processing was created.

### User-defined variables
We can also make up our own variables in three steps:

1. Declare a variable by defining the variable data type and giving a name, and then followed by `;`. What are some possible types? The common data types are `int` and `float`. `int` means interger or a whole number such as 3, -10, 209, etc. `float` means a decimal or floating-point number such as 2.3323093 and -100.334343. A name could be anthing, but usually works with what you're using it for. Here is an example of decalring a variable:

  ```java
  float X;
  float Y;
  ```

2. Iniialize the variable. We give the variable an initial value, which will look like this:

   ```java
    X=width/16;
    Y=height/9;
   ```

3. Use the variable in drawing the small eyeball of the robot face:

   ```java
   ellipse(5.5*X,3*Y,X/4,Y/4);                           
   ```

### Boolean variables
There is a special data type`boolean`. Unlike`int`or`float`, `bloolean`only has two possible values: true or false.


## Conditionals
As mentioned in the Flow section, you can regulate the flow of your program's execution with control statements. One type of control statements is conditional statement.

### If, else if, else
There are `if` `else if` and `else` statements:

```java
If(mouseX>100){
  rect(210, 70, 700, 420, 70);	
}else if(mouseX<50){
  arc(735, 210, 210, 140, PI, 2*PI);   
}else{
  ellipse(385,210,70,140);  
}
```
In this example, if X postion of the mouse is greater than 100 pixels, draw a rectangular. Otherwise if X postion of the mouse is less than 50 pixels, draw an arc. Otherwise, draw an ellipse.

### Boolean expression
In the example above, `mouseX` is a boolean expression. A boolean expression evaluates only to true or false. There are many ways we can create a boolean expression such as using a boolean variable, but the simplest and useful way for us to start with is to use relaitonal operators and logical operators. 

Here are some examples for relational operators: 

`>` greater than

`<` less than

`==` equal to

Here are some examples for logical operators: 

`&&` and

`||` or

```java
if(mouseX>100)||(mouseX<50){
  rect(210, 70, 700, 420, 70);
}

```
This means if X position of the mouse is either greater than 100 pixels or less than 50 pixels, the Processing will draw a rectangular.

## Animated Robot face

With conditional statement, we now have the ability to add some logic to the program and let the program take a path. We can almost make an animated robot face now. Before we can do that, we need to learn the concept of modulo and `map()` function. 

### Modulo
Modulo calculates the remainder when one number is divided by another. For example, when 52.1 is divided by 10, the divisor (10) goes into the dividend (52.1) five times (5 * 10 == 50), and there is a remainder of 2.1 (52.1 - 50 == 2.1). Thus, 52.1 % 10 produces 2.1. In Processing, `%` stands for the modulo operator.

### Map()
`map()` is a calculation fuction allows you to take any range and map a value inside that rang to a new value in any other range. The `map()` calls five arguments and it looks this:

```Java
map(value, start1, stop1, start2, stop2)
```
* "value" is the incoming value to be converted

* "start1" is the lower bound of the value's current range

* "stop1" is the upper bound of the value's current range

* "start2" is the lower bound of the value's target range

* "stop2" is the upper bound of the value's target range



Now we can take what we have learned to make the robots eyes blink and track the mouse movement:

```java
float X;                                                   //create a variable X for better documentation
float Y;

void setup(){
  size(1120,630);
  X=width/16;
  Y=height/9;
}

void draw(){
  background(190);
 
  stroke(1);
  strokeWeight(5);
  fill(255);
  rect(3*X, Y, 10*X, 6*Y, X);                              //draw a face outline
  
   
  if(frameCount % 350>0 && frameCount % 350 <25) {         //if eyes open every 350 frames and stay open for 25 frames, draw eyelids                                 
    strokeWeight(5);
    arc(5.5*X, 3*Y, 3*X, 2*Y, 0,PI);                       //draw right eyelid
    arc(10.5*X, 3*Y, 3*X, 2*Y, 0,PI);                      //draw left eyelid   
    
  }else {                                                  //if not draw eyes open with moving eyeballs 
    strokeWeight(5);
    arc(5.5*X, 3*Y, 3*X, 2*Y, PI, 2*PI);                   //draw right eyelid 
    arc(10.5*X, 3*Y, 3*X, 2*Y, PI, 2*PI);                  //draw left eyelid
   
    fill(0);
    noStroke();
    float eyeballA=map(mouseX,0,width,5*X,6*X);            //The X position of big eyeballs vary with the X position
    ellipse(eyeballA,3*Y,X,1.9*Y);                         //draw right big eyeball
    ellipse(eyeballA+5*X,3*Y,X,1.9*Y);                     //draw left big eyeball
    
    fill(255);
    noStroke();
    float eyeballBX =map(mouseX,0,width,4.9*X,6.1*X);      //The X position of small eyeballs vary with the X position
    float eyeballBY =map(mouseY,0,height,2.25*Y,3.75*Y);   //The Y position of small eyeballs vary with the Y position
    ellipse(eyeballBX,eyeballBY,X/4,Y/4);                  //draw right small eyeball
    ellipse(eyeballBX+5*X,eyeballBY,X/4,Y/4);              //draw left small eyeball

   
  }
  
  fill(255);                                               //draw a mouth
  stroke(1);
  strokeWeight(5);
  arc(8*X,5.3*Y,2*X,Y,0 ,PI);
}
```
![animated robot face](pictures/animated robot face.gif)
## Functions
We have been leanring all this stuff about programming and it's been great, but now comes the time where we need to start to look at tools and ways of organizing our code to make it more scalable for the future. Right now we are just write some variables up at the top and put some suff in `void setup(){}` and `void draw(){}`. It turns out that the `void draw(){}` is getting bigger and bigger and starts to look pretty messy. We need to realize that there are some blocks of the code that draw the eyes, and there are some part of the codes that draw the mouth and face outline. You can atuaclly start to organize you code by creating your own fuctions. 

In fact, you are pretty familiar with the concept of fuctions. When you write the code `background(190)`, you are calling a function. Someone created this fuction and the name it background. This person defined what it means to be background(), and what are the codes should be executed when you, the processing user, call this function.

The way the fuction is defined is by give it a return type and then we have to give it a name of the function. Then we give some amount of arguments and then a open and close curly brackets. Inde the curly brackets, we want to put codes that you want to executed for the function. 

We can now create functions for the robot face, eyes blinking and mouth. The code will look much organized:

```java
float X;                                                   //create a variable X for better documentation
float Y;

void setup(){
  size(1120,630);
  X=width/16;
  Y=height/9;
}

void draw(){
  background(190);
  faceOutline();
  eyesBlink();
  mouth();
  
}
 
void faceOutline(){                                        //draw a face outline
  stroke(1);
  strokeWeight(5);
  fill(255);
  rect(3*X, Y, 10*X, 6*Y, X);                              
} 

void eyesBlink(){   
  if(frameCount % 350>0 && frameCount % 350 <25) {         //if eyes open every 350 frames and stay open for 25 frames, draw eyelids                                 
    strokeWeight(5);
    arc(5.5*X, 3*Y, 3*X, 2*Y, 0,PI);                       //draw right eyelid
    arc(10.5*X, 3*Y, 3*X, 2*Y, 0,PI);                      //draw left eyelid   
    
  }else {                                                  //if not draw eyes open with moving eyeballs 
    strokeWeight(5);
    arc(5.5*X, 3*Y, 3*X, 2*Y, PI, 2*PI);                   //draw right eyelid 
    arc(10.5*X, 3*Y, 3*X, 2*Y, PI, 2*PI);                  //draw left eyelid
   
    fill(0);
    noStroke();
    float eyeballA=map(mouseX,0,width,5*X,6*X);            //The X position of big eyeballs vary with the X position
    ellipse(eyeballA,3*Y,X,1.9*Y);                         //draw right big eyeball
    ellipse(eyeballA+5*X,3*Y,X,1.9*Y);                     //draw left big eyeball
    
    fill(255);
    noStroke();
    float eyeballBX =map(mouseX,0,width,4.9*X,6.1*X);      //The X position of small eyeballs vary with the X position
    float eyeballBY =map(mouseY,0,height,2.25*Y,3.75*Y);   //The Y position of small eyeballs vary with the Y position
    ellipse(eyeballBX,eyeballBY,X/4,Y/4);                  //draw right small eyeball
    ellipse(eyeballBX+5*X,eyeballBY,X/4,Y/4);              //draw left small eyeball

   
  }
}

void mouth(){                                              //draw a mouth
  fill(255);                                               
  stroke(1);
  strokeWeight(5);
  arc(8*X,5.3*Y,2*X,Y,0 ,PI);
}
```


## library
The functions that we've called in the codes are wrritten and defined by someone else ealier. The codes for the functions are stored in the files associated with the Processing software. However, there are tons of other fuctions and feautres that are not included in the software. For example, if you want to make a text box and make the robot talk, you can't really call these functions becuase they don't exist in the Processing software on your computer. Fortunately, someone has already built these features and stored them in the Processing library, you just have to download their codes and import them into your own code file. Let's say we want to build an textbox under the robot face, where users can type whatever they want. Once sumbit it, the robot will open its mouth and speaks whatever is in the textbox. 

### ControlP5
ControlP5, a library wrritten by Andreas Schlegel, allows us to build user interface such as textbox and buttons in Processing. If you go to Sketch/Import Library/Add Library, and then search for ControlP5, you can intall it on your computer and use it in your code. To build a textbox and a submit botton, the code will look like this:

```Java
import controlP5.*;
ControlP5 cp5;
float X;
float Y;


void setup(){
  size(1120,630);
  X=width/16;
  Y=height/9;
  cp5=new ControlP5(this);
  PFont font = createFont("arial", 30);
  
  cp5.addTextfield("")
     .setPosition(0,8*Y)
     .setSize(980,70)
     .setFont(font)
     .setColor(0)
     .setColorBackground(0xffFFFFFF)
     .setColorForeground(0xffFFFFFF)
     .setColorActive(0xff000000)
     .setAutoClear(false);
 
  cp5.addButton("SUBMIT")
     .setPosition(14*X,8*Y)
     .setSize(140,70)
     .setFont(font)
     .setColorLabel(0xffFFFFFF)
     .setColorBackground(0xff565656)
     .setColorForeground(0xff7C7C7C)
     .setColorActive(0xff565656)
     .getCaptionLabel()
     .align(ControlP5.CENTER, ControlP5.CENTER);
} 
```
![Text box and submit botton](pictures/Text box and submit botton.png)

### Ttslib
Ttslib is anohter libarary built by Nikolaus Gradwohl to help make the sketches speak. To import the libary, the code will look like this:

```java
import controlP5.*;
import guru.ttslib.*;
ControlP5 cp5;
TTS tts;
float X;
float Y;

void setup(){
  size(1120,630);
  X=width/16;
  Y=height/9;
  tts = new TTS();
  cp5=new ControlP5(this);
  PFont font = createFont("arial", 30);
  
  cp5.addTextfield("")
     .setPosition(0,8*Y)
     .setSize(980,70)
     .setFont(font)
     .setColor(0)
     .setColorBackground(0xffFFFFFF)
     .setColorForeground(0xffFFFFFF)
     .setColorActive(0xff000000)
     .setAutoClear(false);
 
  cp5.addButton("SUBMIT")
     .setPosition(14*X,8*Y)
     .setSize(140,70)
     .setFont(font)
     .setColorLabel(0xffFFFFFF)
     .setColorBackground(0xff565656)
     .setColorForeground(0xff7C7C7C)
     .setColorActive(0xff565656)
     .getCaptionLabel()
     .align(ControlP5.CENTER, ControlP5.CENTER);
} 
```

## A Talking Robot Face

Now we have set up both libraries but how can we connect them the robot can speak whatever is the in the textbox. Also, it would look more naturally if the mouth moves while the robot speaks. In this case, we need to use boolean variables. As discussed in previous section, a boolean variable can only have to values: true or false. So the program can take a path. Under "true" condition, some codes can be executed such as drawing a open mouth. However, we don't want to draw a open mouth while the robot is not talking, which will be "false" condiiton.

```Java
import controlP5.*;
import guru.ttslib.*;
ControlP5 cp5;
TTS tts;
float X;
float Y;
boolean mouthOpen = false;
boolean speaking = false;

void setup(){
  size(1120,630);
  X=width/16;
  Y=height/9;
  tts = new TTS();
  cp5=new ControlP5(this);
  PFont font = createFont("arial", 30);
  
  cp5.addTextfield("")
     .setPosition(0,8*Y)
     .setSize(980,70)
     .setFont(font)
     .setColor(0)
     .setColorBackground(0xffFFFFFF)
     .setColorForeground(0xffFFFFFF)
     .setColorActive(0xff000000)
     .setAutoClear(false);
 
  cp5.addButton("SUBMIT")
     .setPosition(14*X,8*Y)
     .setSize(140,70)
     .setFont(font)
     .setColorLabel(0xffFFFFFF)
     .setColorBackground(0xff565656)
     .setColorForeground(0xff7C7C7C)
     .setColorActive(0xff565656)
     .getCaptionLabel()
     .align(ControlP5.CENTER, ControlP5.CENTER);
} 

void draw(){
  background(190);
  faceOutline();
  eyesBlink();
  mouth();
  thread("ttsSpeak");
}

void faceOutline(){
  stroke(1);
  strokeWeight(5);
  fill(255);
  rect(3*X, Y, 10*X, 6*Y, X);
}
 
void eyesBlink(){
  if(frameCount % 350>0 && frameCount % 350 <25) {         //eyes open every 350 frames and stay open for 25 frames                                 
    strokeWeight(5);
    arc(5.5*X, 3*Y, 3*X, 2*Y, 0,PI);                       //right eyelid
    arc(10.5*X, 3*Y, 3*X, 2*Y, 0,PI);                      //left eyelid   
    
  }else if(mouseX<14*X || mouseY<8*Y){                     //eyes open with moving eyeballs if the mouse position is outside the SUBMIT botton
    strokeWeight(5);
    arc(5.5*X, 3*Y, 3*X, 2*Y, PI, 2*PI);                   //right eyelid 
    arc(10.5*X, 3*Y, 3*X, 2*Y, PI, 2*PI);                  //left eyelid
   
    fill(0);
    noStroke();
    float eyeballA=map(mouseX,0,width,5*X,6*X);
    ellipse(eyeballA,3*Y,X,1.9*Y);                         //right big eyeball
    ellipse(eyeballA+5*X,3*Y,X,1.9*Y);                     //left big eyeball
    
    fill(255);
    noStroke();
    float eyeballBX =map(mouseX,0,width,4.9*X,6.1*X);
    float eyeballBY =map(mouseY,0,height,2.25*Y,3.75*Y);
    ellipse(eyeballBX,eyeballBY,X/4,Y/4);                  //right small eyeball
    ellipse(eyeballBX+5*X,eyeballBY,X/4,Y/4);              //left small eyeball
    
  }else{                                                   //eyes open with static eyeballs if the mouse position is inside the SUBMIT botton
    strokeWeight(5);
    arc(5.5*X, 3*Y, 3*X, 2*Y, PI, 2*PI);                   //right eyelid 
    arc(10.5*X, 3*Y, 3*X, 2*Y, PI, 2*PI);                  //left eyelid
    
    fill(0);
    noStroke();
    ellipse(5.5*X,3*Y,X,1.9*Y);                            //right big eyeball
    ellipse(10.5*X,3*Y,X,1.9*Y);                           //left big eyeball
    
    fill(255);
    noStroke();
    ellipse(5.5*X,3*Y,X/4,Y/4);                            //right small eyeball
    ellipse(10.5*X,3*Y,X/4,Y/4);                           //left small eyeball
  }   
}
 
void SUBMIT(){                                             //when the SUBMIT button is released, speaking and mouthOpen return true 
  mouthOpen = true; 
  speaking = true;
}

void mouth(){
  if (mouthOpen && frameCount % 40 >0                      //if mouthOpen is true, mouth opens every 40 frames and stays open for 15 frames
      && frameCount % 40 <15){        
    fill(255);
    stroke(1);
    strokeWeight(5);
    arc(8*X,5.3*Y,2*X,2*Y,0 ,PI);                          //lower lip
    
    stroke(1);
    fill(252,50,111);
    arc(8*X,5.3*Y,2*X,2*Y,0.25*PI ,0.75*PI,OPEN);          //tongue
      
    fill(255);
    arc(8*X,5.3*Y,2*X,0.5*Y,PI,2*PI);                      //upper lip   
  }else{                                                   // if mouthOpen is false, mouth closes
    fill(255);
    stroke(1);
    strokeWeight(5);
    arc(8*X,5.3*Y,2*X,Y,0 ,PI);
  }
}

void ttsSpeak(){                                           //if speaking is true, speaking returns false, the robot speaks, and then mouthOpen returns false
  if (speaking){
    speaking = false;
    tts.speak(cp5.get(Textfield.class,"").getText());
    mouthOpen = false;
  }
}

```
![Talking robot](pictures/Talking robot.gif)



