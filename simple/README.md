
### Introductions
About the speaker:
Samanth Martis
Second-year BTech student pursuing Aerospace at IITB
Loves Computational Engineering and Cyber-security.
Fan of physics and math, and likes to draw in spare time.
Studied at TLC-CFAL for 1st and 2nd PUC.
Was in foundation courses before that.
### Aim of the workshop
The whole point of the workshop is to introduce people to simulation using code.
It's a very fun and useful skill/hobby to know and there's no obvious downsides to learning it anyway :)
Additionally, It will also introduce people to a bit of physics and math.
#### What we're going to be today
We will be building a gravity simulator using a language called Javascript. 
We will be using a website for writing our code that removes some 'behind-the-scene' code so that you can focus on the heart of the code that drives the simulator.

We will learn about how Gravity and collision works and how we convert it to code. We will also understand how velocity, position and acceleration are simulated in code.

We will learn basics of Javascript. We will learn logical operators, variables, assignment, classes and functions. 



### Road-map of topics to cover
- Why do we simulate stuff?
- How do we simulate stuff?
- Basic physics and math
- Basic Javascript
- Recap of physics and math
- We start building!
#### Why do we simulate stuff?
 - Costly to test actual models
 - Sometimes it's just impractical. How will you predict if earth will survive getting hit my an asteroid?
 - Simulations also are a way to solve complicated stuff that we can't solve with regular methods.

#### How we're going to simulate stuff
- We're using Javascript, the language that powers the internet.
- Since we can't simulate exact stuff, we are going to do something called 'Discretization'
- We will first learn to draw a circle on the screen
- Next, we will learn how time works in the code
- Next, we will give the circle a velocity
- Next, we will give the circle acceleration
- We will then make another circle and add gravity
- We will combine all the above and complete the simulation!
#### Basic physics and math
 - Newton's laws
 - Gravitation
 - Collision
#### Basic Javascript
- console.log("Hello world");
- variables (let, const, var);
- if-else
#### Recap on physics and math
- Recap on Discretization
- Gravity will update velocity, velocity will update position

#### Build Simulation!

##### Setting up the background!

###### Step1:
Create a canvas of whatever size you want!
```js
function setup() {
  createCanvas(500, 600);
}

function draw() {
  background(220);
}
```
Result: You shoudl see a grey screen show up

###### Step2:
Change background colour to black!

```js
function setup() {
  createCanvas(500, 600);
}

function draw() {
  background("black");
}
```
Result: Your background should now be black


###### STep3:
Change code structure. (Don't worry bout why we do this, but in a nutshell it's to get control of how many times we draw to the screen per second).

We set an interval of 20 milliseconds

```js
function setup() {
  createCanvas(500, 600);
  setInterval(mainCode, 20);
}

function mainCode(){
  background("black");
}
```
Explanation: We tell the program to run the mainCode function every 20 milliseconds

Result: Same black screen as before


##### Drawing a circle!

###### Step1:
We draw a circle using the circle() function. It takes in 3 numbers. The x-coordinate of the circle's center, y-coordinate and diameter.
```js
circle(xCoordinateOfCenter, yCoordinateOfCenter, DiameterOfCircle)
```

Full code:
```js
function setup() {
  createCanvas(500, 600);
  setInterval(mainCode, 20);
}

function mainCode(){
  background("black");
  circle(250, 300, 100)
}
```
Explanation: Here we create a circle of diameter 100 pixels and located at (250, 300)

Result: A white circle is now visible

###### Step2:
Give the circle a colour!
We do that using the fill() function
```js
function setup() {
  createCanvas(500, 600);
  setInterval(mainCode, 20);
}

function mainCode(){
  background("black");
  fill("blue");
  circle(250, 300, 100);
}

```

Result:  A blue circle now appears

##### Giving movement to the circle

###### Step1:
We asign variables for the psoition and radius.
We create three variables with the names c1XPos, c1YPos and c1Rad using the 'let' keyword and assign them values

```js
let c1XPos = 250;
let c1YPos = 300;
let c1Rad = 100;
```

We then use these values when we draw the circle!

```js
circle(c1XPos, c1YPos, 2*c1Rad);
```

```js
let c1XPos = 250;
let c1YPos = 300;
let c1Rad = 100;

function setup() {
  createCanvas(500, 600);
  setInterval(mainCode, 20);
}

function mainCode(){
  background("black");
  fill("blue");
  circle(c1XPos, c1YPos, 2*c1Rad);
}
```
Explanation: Instead of entering direct number values in the circle function, we store the values in 'variables' and then give the variables to the circle function.


Result: The same blue circle


###### Step2:
Increment position!
```js
  c1XPos += 3;
  c1YPos += -2;
```

Full code: 
```js
let c1XPos = 250;
let c1YPos = 300;
let c1Rad = 100;

function setup() {
  createCanvas(500, 600);
  setInterval(mainCode, 20);
}

function mainCode(){
  background("black");
  fill("blue");
  circle(c1XPos, c1YPos, 2*c1Rad);
  c1XPos += 3;
  c1YPos += -2;
}
```
Explanation: Each time the mainCode function is run(it happens ever 20ms), the x and y positions are incremented by 3 and -2 respectively.

Result: The circle now moves


###### Step3:
Create variables and set them to the velocity

```js
let c1XVel = 3;
let c1YVel = -2;
```

Then, increment the positions using the velocity instead of hard-coded numbers.

```js
  c1XPos += c1XVel;
  c1YPos += c1YVel;
```


Full code:
```js
let c1XPos = 250;
let c1YPos = 300;
let c1XVel = 3;
let c1YVel = -2;
let c1Rad = 100;


function setup() {
  createCanvas(500, 600);
  setInterval(mainCode, 20);
}

function mainCode(){
  background("black");
  fill("blue");
  circle(c1XPos, c1YPos, 2*c1Rad);
  c1XPos += c1XVel;
  c1YPos += c1YVel;
}

```

Explanation: We did a similar thing to position. Instead of writing the position directly, we stored the value in a variable and then used it. SImilarly here, we store the velocity values in variables and then use it to increment the position.

Result: Same moving circle


###### Step4:
Add acceleration!
Just like how we updated position using velocity, we update velocity using acceleration!
```js
  c1XVel += 0.02;
  c1YVel += 0.1;
```
We can then also replace them with variables.
```js
let c1XAcc = 0.02;
let c1YAcc = 0.1;
```
```js
  c1XVel += c1XAcc;
  c1YVel += c1YAcc;
```

Full code:
```js
let c1XPos = 250;
let c1YPos = 300;
let c1XVel = 3;
let c1YVel = -2;
let c1XAcc = 0.02;
let c1YAcc = 0.1;
let c1Rad = 100;


function setup() {
  createCanvas(500, 600);
  setInterval(mainCode, 20);
}

function mainCode(){
  background("black");
  fill("blue");
  circle(c1XPos, c1YPos, 2*c1Rad);
  c1XPos += c1XVel;
  c1YPos += c1YVel;
  c1XVel += c1XAcc;
  c1YVel += c1YAcc;
  
}
```

Result: The circle now follows a curved path

###### Step5:
Change values so that it falls down
For this we make X velocity and acceleration 0 and Y acceleration positive (downward)
```js
let c1XPos = 250;
let c1YPos = 300;
let c1XVel = 0;
let c1YVel = -10;
let c1XAcc = 0;
let c1YAcc = 0.5;
let c1Rad = 100;
```
We also great a variable g that stores gravity value. 
```js
let g = 0.5;
```
We then equate Y acceleration to g

```js
let c1YAcc = g;
```

Full code:
```js
let g = 0.5;

let c1XPos = 250;
let c1YPos = 300;
let c1XVel = 0;
let c1YVel = -10;
let c1XAcc = 0;
let c1YAcc = g;
let c1Rad = 100;


function setup() {
  createCanvas(500, 600);
  setInterval(mainCode, 20);
}

function mainCode(){
  background("black");
  fill("blue");
  circle(c1XPos, c1YPos, 2*c1Rad);
  c1XPos += c1XVel;
  c1YPos += c1YVel;
  c1XVel += c1XAcc;
  c1YVel += c1YAcc;
  
}
```

Result: The circle now goes up for a while but then falls down


##### Make the circle bounce!
Theory: If I'm hitting the bottom or top wall and the collision is perfectly 'elastic', I would expect the vertical velocity to get exactly reversed. Similarly, if hitting the right or left wall, the X velocity would get reversed.

First we need to detect the collision, and then we need to flip the correct velocity!

###### Step1:
Get coordinates of walls. 
We will make the walls be our canvas. So let's create two variables for canvas size and enter it when we use the createCanvas function
```js
let canvasWidth = 500;
let canvasHeight = 600;
```

```js
createCanvas(canvasWidth, canvasHeight);
```
full code:
```js
let g = 0.5;

let c1XPos = 250;
let c1YPos = 300;
let c1XVel = 0;
let c1YVel = -10;
let c1XAcc = 0;
let c1YAcc = g;
let c1Rad = 100;

let canvasWidth = 500;
let canvasHeight = 600;

function setup() {
  createCanvas(canvasWidth, canvasHeight);
  setInterval(mainCode, 20);
}

function mainCode(){
  background("black");
  fill("blue");
  circle(c1XPos, c1YPos, 2*c1Rad);
  c1XPos += c1XVel;
  c1YPos += c1YVel;
  c1XVel += c1XAcc;
  c1YVel += c1YAcc;
  
}

```


We now know the coordinates of the wall.

###### Step2:
Bottom wall collision detection.

One possible way you would think of detecting collision is by checking if the c1YPos is more than the height of the canvas, ie, its past the wall. 
If the value is more than the wall, then we flip velocity.
We would implement this using an 'if-condition'

```js
  if(c1YPos>canvasHeight){
    c1YVel *= -1;
  }
```
Full code:
```js
let g = 0.5;

let c1XPos = 250;
let c1YPos = 300;
let c1XVel = 0;
let c1YVel = -10;
let c1XAcc = 0;
let c1YAcc = g;
let c1Rad = 100;

let canvasWidth = 500;
let canvasHeight = 600;

function setup() {
  createCanvas(canvasWidth, canvasHeight);
  setInterval(mainCode, 20);
}

function mainCode(){
  background("black");
  fill("blue");
  circle(c1XPos, c1YPos, 2*c1Rad);
  c1XPos += c1XVel;
  c1YPos += c1YVel;
  if(c1YPos>canvasHeight){
    c1YVel *= -1;
  }
  c1XVel += c1XAcc;
  c1YVel += c1YAcc;
  

  
}
```

Result: The ball now bounces but there's something a bit off.


###### Step2:
Fix error.

there is a mistake in what we did. If you look carefully, you'll notice that the ball goes halfway into the border and only then bounces. 

This happens because we're checking if the center of the circle has crossed the wall. We shoud instead be checking if the edge of the ball has crossed the wall.

We can easily do by changing 
```js
if(c1YPos>canvasHeight)
```
to

```js
if((c1YPos+c1Rad)>canvasHeight)
```

Additionally, we also have to set the position of the ball such that it doesn't merge with the wall.

We do both of the above as follows:
```js
  if((c1YPos+c1Rad)>canvasHeight){
    c1YVel *= -1;
    c1YPos = canvasHeight - c1Rad;
  }
```

Full code:
```js
let g = 0.5;

let c1XPos = 250;
let c1YPos = 300;
let c1XVel = 0;
let c1YVel = -10;
let c1XAcc = 0;
let c1YAcc = g;
let c1Rad = 100;

let canvasWidth = 500;
let canvasHeight = 600;

function setup() {
  createCanvas(canvasWidth, canvasHeight);
  setInterval(mainCode, 20);
}

function mainCode(){
  background("black");
  fill("blue");
  circle(c1XPos, c1YPos, 2*c1Rad);
  c1XPos += c1XVel;
  c1YPos += c1YVel;
  if((c1YPos+c1Rad)>canvasHeight){
    c1YVel *= -1;
    c1YPos = canvasHeight - c1Rad;
  }
  c1XVel += c1XAcc;
  c1YVel += c1YAcc;
  
}

```

###### Step3:
Add conditions for other walls

```js
  if((c1YPos+c1Rad)>canvasHeight){
    c1YVel *= -1;
    c1YPos = canvasHeight - c1Rad;
  }
  if((c1YPos-c1Rad)<0){
    c1YVel *= -1;
    c1YPos = c1Rad;
  }
  if((c1XPos+c1Rad)>canvasWidth){
    c1XVel *= -1;
    c1XPos = canvasWidth - c1Rad;
  }
  if((c1XPos-c1Rad)<0){
    c1XVel *= -1;
    c1XPos = c1Rad;
  }
  ```

  Once the conditions are added, we can also change the starting velocity and radius to make it more obvious that our code is working!

  ```js
let c1XVel = 10;
let c1YVel = -15;
let c1Rad = 10;
  ```

Full code
```js
let g = 0.5;

let c1XPos = 250;
let c1YPos = 300;
let c1XVel = 10;
let c1YVel = -15;
let c1XAcc = 0;
let c1YAcc = g;
let c1Rad = 10;

let canvasWidth = 500;
let canvasHeight = 600;

function setup() {
  createCanvas(canvasWidth, canvasHeight);
  setInterval(mainCode, 20);
}

function mainCode(){
  background("black");
  fill("blue");
  circle(c1XPos, c1YPos, 2*c1Rad);
  c1XPos += c1XVel;
  c1YPos += c1YVel;
  if((c1YPos+c1Rad)>canvasHeight){
    c1YVel *= -1;
    c1YPos = canvasHeight - c1Rad;
  }
  if((c1YPos-c1Rad)<0){
    c1YVel *= -1;
    c1YPos = c1Rad;
  }
  if((c1XPos+c1Rad)>canvasWidth){
    c1XVel *= -1;
    c1XPos = canvasWidth - c1Rad;
  }
  if((c1XPos-c1Rad)<0){
    c1XVel *= -1;
    c1XPos = c1Rad;
  }
 
  c1XVel += c1XAcc;
  c1YVel += c1YAcc;
  
}

```


##### Add another ball!

Copy paste the variables and maincode but change c1 to c2!

Also change its initial starting position and velocity



full code
```js
let g = 0.5;

let c1XPos = 250;
let c1YPos = 300;
let c1XVel = 10;
let c1YVel = -15;
let c1XAcc = 0;
let c1YAcc = g;
let c1Rad = 10;

let c2XPos = 200;
let c2YPos = 350;
let c2XVel = 10;
let c2YVel = -15;
let c2XAcc = 0;
let c2YAcc = g;
let c2Rad = 10;

let canvasWidth = 500;
let canvasHeight = 600;

function setup() {
  createCanvas(canvasWidth, canvasHeight);
  setInterval(mainCode, 20);
}

function mainCode(){
  background("black");
  fill("blue");
  circle(c1XPos, c1YPos, 2*c1Rad);
  c1XPos += c1XVel;
  c1YPos += c1YVel;
  if((c1YPos+c1Rad)>canvasHeight){
    c1YVel *= -1;
    c1YPos = canvasHeight - c1Rad;
  }
  if((c1YPos-c1Rad)<0){
    c1YVel *= -1;
    c1YPos = c1Rad;
  }
  if((c1XPos+c1Rad)>canvasWidth){
    c1XVel *= -1;
    c1XPos = canvasWidth - c1Rad;
  }
  if((c1XPos-c1Rad)<0){
    c1XVel *= -1;
    c1XPos = c1Rad;
  }
 
  c1XVel += c1XAcc;
  c1YVel += c1YAcc;
  
  
  fill("yellow");
  circle(c2XPos, c2YPos, 2*c2Rad);
  c2XPos += c2XVel;
  c2YPos += c2YVel;
  if((c2YPos+c2Rad)>canvasHeight){
    c2YVel *= -1;
    c2YPos = canvasHeight - c2Rad;
  }
  if((c2YPos-c2Rad)<0){
    c2YVel *= -1;
    c2YPos = c2Rad;
  }
  if((c2XPos+c2Rad)>canvasWidth){
    c2XVel *= -1;
    c2XPos = canvasWidth - c2Rad;
  }
  if((c2XPos-c2Rad)<0){
    c2XVel *= -1;
    c2XPos = c2Rad;
  }
 
  c2XVel += c2XAcc;
  c2YVel += c2YAcc;
  
}

```
Result: Two balls now visible moving. One yellow and one blue



