
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
We will be building an Earth-Moon gravity simulator using a language called Javascript.
We will be using a website for writing our code that removes some 'behind-the-scene' code so that you can focus on the heart of the code that drives the simulator.

We will learn about how Gravity works and how we convert it to code. We will also understand how velocity, position and acceleration are simulated in code.

We will learn basics of Javascript. We will learn logical operators, variables, assignment, classes and functions. 

If time permits, we will also be making a 20-body simulator and a collision-simulation!

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
- We're going to be building a less accurate, but more easier version of Earth and Moon.
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
 - Calculus(a bit only)
 - Trignometry
#### Basic Javascript
- console.log("Hello world");
- variables (let, const, var);
- Classes
- RGB colours
- Loops, Intervals
#### Recap on physics and math
- Recap on Discretization
- Gravity will update velocity, velocity will update position

#### Build Simulation!


Main step1: Draw a circle

Step1:
Create a canvas with a black background!

```js
function setup() {
  createCanvas(400, 400);
}

function draw() {
  background(0);
}
```




Step2
Make the canvas as big as the window
```js
function setup() {
  createCanvas(window.innerWidth, window.innerHeight);
}

function draw() {
  background(0);
}
```



Step3
Draw a circle at the center of canvas
```js
function setup() {
  createCanvas(window.innerWidth, window.innerHeight);
}

function draw() {
  background(0);
  circle(canvas.width/2, canvas.height/2, 100);
}
```

Step4
Add colour!
```js
function setup() {
  createCanvas(window.innerWidth, window.innerHeight);
}

function draw() {
  background(0);
  fill(0, 0, 255);
  circle(canvas.width/2, canvas.height/2, 100);
}
```

Result:
\<Enter Completed circle image>


Main Step2:
Give the circle velocity

step1: Create variables for circle position
```js
let circleXPosition;
let circleYPosition;

function setup() {
  createCanvas(window.innerWidth, window.innerHeight);
}

function draw() {
  
  background(0);
  fill(0, 0, 255);
  circle(canvas.width/2, canvas.height/2, 100);
}
```

Step2:
Assign the variables with their values.

```js
let circleXPosition;
let circleYPosition;

function setup() {
  createCanvas(window.innerWidth, window.innerHeight);
  circleXPosition = canvas.width/2;
  circleYPosition = canvas.height/2;
}

function draw() {
  
  background(0);
  fill(0, 0, 255);
  circle(canvas.width/2, canvas.height/2, 100);
}
```

Step3:
Use the position when drawing the circle
```js
let circleXPosition;
let circleYPosition;

function setup() {
  createCanvas(window.innerWidth, window.innerHeight);
  circleXPosition = canvas.width/2;
  circleYPosition = canvas.height/2;
}

function draw() {
  
  background(0);
  fill(0, 0, 255);
  circle(circleXPosition, circleYPosition, 100);
}
```

Step4:
Update the position by a fixed amount every time the draw function is used

```js
let circleXPosition;
let circleYPosition;

function setup() {
  createCanvas(window.innerWidth, window.innerHeight);
  circleXPosition = canvas.width/2;
  circleYPosition = canvas.height/2;
}

function draw() {
  
  background(0);
  fill(0, 0, 255);
  circle(circleXPosition, circleYPosition, 100);
  circleXPosition += 2;
  circleYPosition -= 3
}
```


Step4:
Create an use variables for velocity. Note, the below code is 'wrong', but we will correct it later
```js
let circleXPosition;
let circleYPosition;
let circleXVelocity;
let circleYVelocity;

function setup() {
  createCanvas(window.innerWidth, window.innerHeight);
  circleXPosition = canvas.width/2;
  circleYPosition = canvas.height/2;
  circleXVelocity = 3;
  circleYVelocity = -5;
}

function draw() {
  
  background(0)
  fill(0, 0, 255);
  circle(circleXPosition, circleYPosition, 100);
  circleXPosition += circleXVelocity;
  circleYPosition += circleYVelocity;
}
```
The above is wrong because we aren't accounting for time. The units of measurements here are in pixels. Velocity is in pixels/second, not meters/second


Step5:
Find time. We use performance.now() to get time. Notice that we care about change in time more.
```js
let circleXPosition;
let circleYPosition;
let circleXVelocity;
let circleYVelocity;
let time1;
let time2;
let timePassed;

function setup() {
  createCanvas(window.innerWidth, window.innerHeight);
  circleXPosition = canvas.width/2;
  circleYPosition = canvas.height/2;
  circleXVelocity = 3;
  circleYVelocity = -5;
  time1 = performace.now();
}

function draw() {
  
  background(0)
  fill(0, 0, 255);
  circle(circleXPosition, circleYPosition, 100);
  
  time2 = performance.now();
  timePassed = (time2 - time1)/1000; //We divide by 1000 to convert from milli-seconds to seconds
  time1 = time2;
  
  circleXPosition += circleXVelocity;
  circleYPosition += circleYVelocity;
}
```


Step6:
We use the time passed in our calculation. We also change the velocity values to a proper size

```js
let circleXPosition;
let circleYPosition;
let circleXVelocity;
let circleYVelocity;
let time1;
let time2;
let timePassed;

function setup() {
  createCanvas(window.innerWidth, window.innerHeight);
  circleXPosition = canvas.width/2;
  circleYPosition = canvas.height/2;
  circleXVelocity = 300;
  circleYVelocity = -500;
  time1 = performance.now();
}

function draw() {
  
  background(0)
  fill(0, 0, 255);
  circle(circleXPosition, circleYPosition, 100);
  
  time2 = performance.now();
  timePassed = (time2 - time1)/1000;
  time1 = time2;
  
  circleXPosition += circleXVelocity*timePassed;
  circleYPosition += circleYVelocity*timePassed;
}
```

Result:
Circle now has velocity


Main step3:
Give circle acceleration

Step1:
Create variables for acceleration and assign them a value
```js
let circleXPosition;
let circleYPosition;
let circleXVelocity;
let circleYVelocity;
let time1;
let time2;
let timePassed;
let circleXAcceleration;
let circleYAcceleration;

function setup() {
  createCanvas(window.innerWidth, window.innerHeight);
  circleXPosition = canvas.width/2;
  circleYPosition = canvas.height/2;
  circleXVelocity = 300;
  circleYVelocity = -500;
  circleXAcceleration = 0;
  circleYAcceleration = 700;
  time1 = performance.now();
  
}

function draw() {
  
  background(0)
  fill(0, 0, 255);
  circle(circleXPosition, circleYPosition, 100);
  
  time2 = performance.now();
  timePassed = (time2 - time1)/1000;
  time1 = time2;

  
  
  circleXPosition += circleXVelocity*timePassed;
  circleYPosition += circleYVelocity*timePassed;
}
```

Step2: 
Similar to how we update position using velocity, we update velocity using acceleration!

```js
let circleXPosition;
let circleYPosition;
let circleXVelocity;
let circleYVelocity;
let time1;
let time2;
let timePassed;
let circleXAcceleration;
let circleYAcceleration;

function setup() {
  createCanvas(window.innerWidth, window.innerHeight);
  circleXPosition = canvas.width/2;
  circleYPosition = canvas.height/2;
  circleXVelocity = 300;
  circleYVelocity = -500;
  circleXAcceleration = 0;
  circleYAcceleration = 700;
  time1 = performance.now();
  
}

function draw() {
  
  background(0)
  fill(0, 0, 255);
  circle(circleXPosition, circleYPosition, 100);
  
  time2 = performance.now();
  timePassed = (time2 - time1)/1000;
  time1 = time2;
  


  circleXVelocity += circleXAcceleration*timePassed;
  circleYVelocity += circleYAcceleration*timePassed;
  
  
  circleXPosition += circleXVelocity*timePassed;
  circleYPosition += circleYVelocity*timePassed;
}

```

Result:
Circle now appears to fall!


Main Step3:
Make code cleaner using classes


Step1:
Create planet Class and add a 'constructor' to it. Dont worry about what the constructor is right now.

```js
let circleXPosition;
let circleYPosition;
let circleXVelocity;
let circleYVelocity;
let time1;
let time2;
let timePassed;
let circleXAcceleration;
let circleYAcceleration;

class Planet{
  constructor(){}
}

//... Rest of the code

```

Step2:
Create position and velocity variables Assign them some default values
```js
class Planet{
  constructor(){
    this.XPosition = 0;
    this.YPosition = 0;
    this.XVelocity = 0;
    this.YVelocity = 0;
    this.XAcceleration = 0;
    this.YAcceleration = 0;
    this.size = 0;
    this.colour = "white";
  }
}
```

Step3:
Create a new planet. We do that using the 'new' keyword
```js
let Earth;
function setup(){
	Earth = new Planet();
}
```
Full code:
```js
let circleXPosition;
let circleYPosition;
let circleXVelocity;
let circleYVelocity;
let time1;
let time2;
let timePassed;
let circleXAcceleration;
let circleYAcceleration;

let Earth;

class Planet{
  constructor(){
    this.XPosition = 0;
    this.YPosition = 0;
    this.XVelocity = 0;
    this.YVelocity = 0;
    this.XAcceleration = 0;
    this.YAcceleration = 0;
    this.size = 0;
    this.colour = "white";
  }
}


function setup() {
  createCanvas(window.innerWidth, window.innerHeight);
  circleXPosition = canvas.width/2;
  circleYPosition = canvas.height/2;
  circleXVelocity = 300;
  circleYVelocity = -500;
  circleXAcceleration = 0;
  circleYAcceleration = 700;
  time1 = performance.now();
  Earth = new Planet();
}

function draw() {
  background(0)
  fill(0, 0, 255);
  circle(circleXPosition, circleYPosition, 100);
  time2 = performance.now();
  timePassed = (time2 - time1)/1000;
  time1 = time2;
  circleXVelocity += circleXAcceleration*timePassed;
  circleYVelocity += circleYAcceleration*timePassed;
  circleXPosition += circleXVelocity*timePassed;
  circleYPosition += circleYVelocity*timePassed;
}
```

Step4:
Setup initial values(properties) of Earth. We do that using the dot ' . '
We do this in the setup() function
```js
  Earth.XPosition = canvas.width/2;
  Earth.YPosition = canvas.height/2;
  Earth.XVelocity = 300;
  Earth.YVelocity = -500;
  Earth.size = 100;
  Earth.colour = "blue";
```

Full code:
```js
let circleXPosition;
let circleYPosition;
let circleXVelocity;
let circleYVelocity;
let time1;
let time2;
let timePassed;
let circleXAcceleration;
let circleYAcceleration;

let Earth;

class Planet{
  constructor(){
    this.XPosition = 0;
    this.YPosition = 0;
    this.XVelocity = 0;
    this.YVelocity = 0;
    this.size = 0;
    this.colour = "white";
  }
}


function setup() {
  createCanvas(window.innerWidth, window.innerHeight);
  circleXPosition = canvas.width/2;
  circleYPosition = canvas.height/2;
  circleXVelocity = 300;
  circleYVelocity = -500;
  circleXAcceleration = 0;
  circleYAcceleration = 700;
  time1 = performance.now();
  Earth = new Planet();
  Earth.XPosition = canvas.width/2;
  Earth.YPosition = canvas.height/2;
  Earth.XVelocity = 300;
  Earth.YVelocity = -500;
  Earth.size = 100;
  Earth.colour = "blue";
  
  
}

function draw() {
  background(0)
  fill(0, 0, 255);
  circle(circleXPosition, circleYPosition, 100);
  time2 = performance.now();
  timePassed = (time2 - time1)/1000;
  time1 = time2;
  circleXVelocity += circleXAcceleration*timePassed;
  circleYVelocity += circleYAcceleration*timePassed;
  circleXPosition += circleXVelocity*timePassed;
  circleYPosition += circleYVelocity*timePassed;
}

```


Step5: Replace circle variables with Earth

```js
let time1;
let time2;
let timePassed;
let Earth;

class Planet{
  constructor(){
    this.XPosition = 0;
    this.YPosition = 0;
    this.XVelocity = 0;
    this.YVelocity = 0;
    this.XAcceleration = 0;
    this.YAcceleration = 0;
    this.size = 0;
    this.colour = "white";
  }
}


function setup() {
  createCanvas(window.innerWidth, window.innerHeight);
  time1 = performance.now();
  Earth = new Planet();
  Earth.XPosition = canvas.width/2;
  Earth.YPosition = canvas.height/2;
  Earth.XVelocity = 300;
  Earth.YVelocity = -500;
  Earth.XAcceleration = 0;
  Earth.YAcceleration = 700;
  Earth.size = 100;
  Earth.colour = "blue";
}

function draw() {
  background(0)
  fill(Earth.colour);
  circle(Earth.XPosition, Earth.YPosition, Earth.size);
  time2 = performance.now();
  timePassed = (time2 - time1)/1000;
  time1 = time2;
  Earth.XVelocity += Earth.XAcceleration*timePassed;
  Earth.YVelocity += Earth.YAcceleration*timePassed;
  Earth.XPosition += Earth.XVelocity*timePassed;
  Earth.YPosition += Earth.YVelocity*timePassed;
}
```


Step6: Use constructor
Instead of assigning values separately, we can do it when we create the planet itself using the constructor

We do this by 'passing parameters'
```js

class Planet{
  constructor(firstValue, secondValue, thirdValue, fourthValue, fifthValue, sixthValue, seventhValue, eigthValue, ninthvalue){
    this.XPosition = firstValue;
    this.YPosition = secondValue;
    this.XVelocity = thirdValue;
    this.YVelocity = fourthValue;
    this.XAcceleration = fifthValue;
    this.YAcceleration = sixthValue;
    this.size = seventhValue;
    this.colour = eigthValue;
    this.mass = ninthValue
  }
}
```
Note, you don't have to name then firstvalue, secondValue etc etc... U can name them anything. The order is important.

Once we do this, when we create the planet, we pass in extra data
```js
Earth = new Planet(canvas.width/2, canvas.height/2, 300, -500, 0, 700, 100, "blue", 2000);
```

Full code:
```js
let time1;
let time2;
let timePassed;
let Earth;

class Planet{
  constructor(firstValue, secondValue, thirdValue, fourthValue, fifthValue, sixthValue, seventhValue, eigthValue, ninthValue){
    this.XPosition = firstValue;
    this.YPosition = secondValue;
    this.XVelocity = thirdValue;
    this.YVelocity = fourthValue;
    this.XAcceleration = fifthValue;
    this.YAcceleration = sixthValue;
    this.size = seventhValue;
    this.colour = eigthValue;
    this.mass = ninthValue;
  }
}

function setup() {
  createCanvas(window.innerWidth, window.innerHeight);
  time1 = performance.now();
  Earth = new Planet(canvas.width/2, canvas.height/2, 300, -500, 0, 700, 100, "blue", 2000);
}

function draw() {
  background(0)
  fill(Earth.colour);
  circle(Earth.XPosition, Earth.YPosition, Earth.size);
  time2 = performance.now();
  timePassed = (time2 - time1)/1000;
  time1 = time2;
  Earth.XVelocity += Earth.XAcceleration*timePassed;
  Earth.YVelocity += Earth.YAcceleration*timePassed;
  Earth.XPosition += Earth.XVelocity*timePassed;
  Earth.YPosition += Earth.YVelocity*timePassed;
}
```
Notice how we did all of the assignment in one line!

Result:
Same circle but now using classes

Main step4:
Make the moon

Since we spent extra effort in making classes and constructors, our work is now much easier.

Step 1;
Create a moon variable
```js
let Moon;
```

Make it a planet in the setup function. Give it some values.
```js
Moon = new Planet(canvas.width/2 - 300, canvas.height/2, 0, 100, 0, -100, 20, "white", 250);
```
Then duplicate the process of updating velocities and positions with the moon.

```js
  fill(Moon.colour);
  circle(Moon.XPosition, Moon.YPosition, Moon.size);
  Moon.XVelocity += Moon.XAcceleration*timePassed;
  Moon.YVelocity += Moon.YAcceleration*timePassed;
  Moon.XPosition += Moon.XVelocity*timePassed;
  Moon.YPosition += Moon.YVelocity*timePassed;
```


Full code (Note, a bit of rearrangement was made):
```js
let time1;
let time2;
let timePassed;
let Earth;
let Moon;

class Planet{
  constructor(firstValue, secondValue, thirdValue, fourthValue, fifthValue, sixthValue, seventhValue, eigthValue, ninthValue){
    this.XPosition = firstValue;
    this.YPosition = secondValue;
    this.XVelocity = thirdValue;
    this.YVelocity = fourthValue;
    this.XAcceleration = fifthValue;
    this.YAcceleration = sixthValue;
    this.size = seventhValue;
    this.colour = eigthValue;
    this.mass = ninthValue
  }
}


function setup() {
  createCanvas(window.innerWidth, window.innerHeight);
  time1 = performance.now();
  Earth = new Planet(canvas.width/2, canvas.height/2, 300, -500, 0, 700, 100, "blue", 2000);
  Moon = new Planet(canvas.width/2 - 300, canvas.height/2, 0, 100, 0, -100, 20, "white", 250);
}

function draw() {
  background(0)
  
  
  time2 = performance.now();
  timePassed = (time2 - time1)/1000;
  time1 = time2;
  
  
  fill(Earth.colour);
  circle(Earth.XPosition, Earth.YPosition, Earth.size);
  Earth.XVelocity += Earth.XAcceleration*timePassed;
  Earth.YVelocity += Earth.YAcceleration*timePassed;
  Earth.XPosition += Earth.XVelocity*timePassed;
  Earth.YPosition += Earth.YVelocity*timePassed;
  
  fill(Moon.colour);
  circle(Moon.XPosition, Moon.YPosition, Moon.size);
  Moon.XVelocity += Moon.XAcceleration*timePassed;
  Moon.YVelocity += Moon.YAcceleration*timePassed;
  Moon.XPosition += Moon.XVelocity*timePassed;
  Moon.YPosition += Moon.YVelocity*timePassed;
}
```


Result:
Now two circles are seen on the screen. One blue and big, the other white and small.


Main step5:
Implement Gravity.


Step1:
Calculate distance using Pythagoras theorem. We do this in the draw() loop since the distance keeps changing. 
If we want, we can console.log(distance) to see that it's working.
```js
//Note the d in dy stands for delta, meaning change
  let dx = Moon.XPosition - Earth.XPosition;
  let dy = Moon.YPosition - Earth.YPosition;
  let distance = sqrt(dx**2 + dy**2);
  //console.log(distance);
```

Step2:
Calculate force using $F = G\frac{{ m_{1}m_{2}}}{r^2}$
We also create a variable G
```js
let G = 10000;
```

```js
let force = G*Earth.mass*Moon.mass/(distance**2);
```
Now, we find the angle of the the atan2 function. Don't worry about it too much. It takes in dy and dx and returns the angle.
```js
let angle = atan2(dy, dx);
```

Full code:
```js
let time1;
let time2;
let timePassed;
let Earth;
let Moon;
let G;

class Planet{
  constructor(firstValue, secondValue, thirdValue, fourthValue, fifthValue, sixthValue, seventhValue, eigthValue, ninthValue){
    this.XPosition = firstValue;
    this.YPosition = secondValue;
    this.XVelocity = thirdValue;
    this.YVelocity = fourthValue;
    this.XAcceleration = fifthValue;
    this.YAcceleration = sixthValue;
    this.size = seventhValue;
    this.colour = eigthValue;
    this.mass = ninthValue
  }
}


function setup() {
  createCanvas(window.innerWidth, window.innerHeight);
  G = 10000;
  time1 = performance.now();
  Earth = new Planet(canvas.width/2, canvas.height/2, 300, -500, 0, 700, 100, "blue", 2000);
  Moon = new Planet(canvas.width/2 - 300, canvas.height/2, 0, 100, 0, -100, 20, "white", 250);
}

function draw() {
  background(0)
  
  
  time2 = performance.now();
  timePassed = (time2 - time1)/1000;
  time1 = time2;
  
  let dx = Moon.XPosition - Earth.XPosition;
  let dy = Moon.YPosition - Earth.YPosition;
  let distance = Math.sqrt(dx**2 + dy**2);
  let force = G*Earth.mass*Moon.mass/(distance**2);

  
  fill(Earth.colour);
  circle(Earth.XPosition, Earth.YPosition, Earth.size);
  Earth.XVelocity += Earth.XAcceleration*timePassed;
  Earth.YVelocity += Earth.YAcceleration*timePassed;
  Earth.XPosition += Earth.XVelocity*timePassed;
  Earth.YPosition += Earth.YVelocity*timePassed;
  
  fill(Moon.colour);
  circle(Moon.XPosition, Moon.YPosition, Moon.size);
  Moon.XVelocity += Moon.XAcceleration*timePassed;
  Moon.YVelocity += Moon.YAcceleration*timePassed;
  Moon.XPosition += Moon.XVelocity*timePassed;
  Moon.YPosition += Moon.YVelocity*timePassed;
}
```



Step3:
Add a limit to the force to prevent simulation from breaking.
```js
  if(force>300000){
    force = 300000;
  }
```

Step4:
Use Trignometry and update the accelerations.

```js
  Earth.XAcceleration = force*cos(angle) / Earth.mass;
  Earth.YAcceleration = force*sin(angle) / Earth.mass;
  Moon.XAcceleration = -force*cos(angle) / Moon.mass;
  Moon.YAcceleration = -force*sin(angle) / Moon.mass;
```

Optional step: Set initial velocities of earth and moon as zero.

Final code: 
```js
let time1;
let time2;
let timePassed;
let Earth;
let Moon;
let G;

class Planet{
  constructor(firstValue, secondValue, thirdValue, fourthValue, fifthValue, sixthValue, seventhValue, eigthValue, ninthValue){
    this.XPosition = firstValue;
    this.YPosition = secondValue;
    this.XVelocity = thirdValue;
    this.YVelocity = fourthValue;
    this.XAcceleration = fifthValue;
    this.YAcceleration = sixthValue;
    this.size = seventhValue;
    this.colour = eigthValue;
    this.mass = ninthValue
  }
}


function setup() {
  createCanvas(window.innerWidth, window.innerHeight);
  G = 10000
  time1 = performance.now();
  Earth = new Planet(canvas.width/2, canvas.height/2, 0.0, -0.00, 0, 700, 100, "blue", 2000);
  Moon = new Planet(canvas.width/2 - 300, canvas.height/2, 0, 0, 0, -100, 20, "white", 250);
}

function draw() {
  background(0);
  
  
  time2 = performance.now();
  timePassed = (time2 - time1)/1000;
  time1 = time2;
  
  let dx = Moon.XPosition - Earth.XPosition;
  let dy = Moon.YPosition - Earth.YPosition;
  let distance = sqrt(dx**2 + dy**2);
  let force = G*Earth.mass*Moon.mass/(distance**2);
  let angle = atan2(dy, dx);
  
  if(force>300000){
    force = 300000;
  }
  
  Earth.XAcceleration = force*cos(angle) / Earth.mass;
  Earth.YAcceleration = force*sin(angle) / Earth.mass;
  Moon.XAcceleration = -force*cos(angle) / Moon.mass;
  Moon.YAcceleration = -force*sin(angle) / Moon.mass;
  
  
  fill(Earth.colour);
  circle(Earth.XPosition, Earth.YPosition, Earth.size);
  Earth.XVelocity += Earth.XAcceleration*timePassed;
  Earth.YVelocity += Earth.YAcceleration*timePassed;
  Earth.XPosition += Earth.XVelocity*timePassed;
  Earth.YPosition += Earth.YVelocity*timePassed;
  
  fill(Moon.colour);
  circle(Moon.XPosition, Moon.YPosition, Moon.size);
  Moon.XVelocity += Moon.XAcceleration*timePassed;
  Moon.YVelocity += Moon.YAcceleration*timePassed;
  Moon.XPosition += Moon.XVelocity*timePassed;
  Moon.YPosition += Moon.YVelocity*timePassed;
}
```
Tada! You have completed the simulation!

Now we just choose the appropriate values and make it look good!

Optional: 
Add a speedup variable
```js
let speedup = 3;
```
```js
timePassed = speedup*(time2 - time1)/1000;

```



Final working code:
```js
let time1;
let time2;
let timePassed;
let Earth;
let Moon;
let G;
let speedup = 3;

class Planet{
  constructor(firstValue, secondValue, thirdValue, fourthValue, fifthValue, sixthValue, seventhValue, eigthValue, ninthValue){
    this.XPosition = firstValue;
    this.YPosition = secondValue;
    this.XVelocity = thirdValue;
    this.YVelocity = fourthValue;
    this.XAcceleration = fifthValue;
    this.YAcceleration = sixthValue;
    this.size = seventhValue;
    this.colour = eigthValue;
    this.mass = ninthValue
  }
}


function setup() {
  createCanvas(window.innerWidth, window.innerHeight);
  G = 10000
  time1 = performance.now();
  Earth = new Planet(canvas.width/2, canvas.height/2, 0.0, -25, 0, 700, 100, "blue", 2000);
  Moon = new Planet(canvas.width/2 - 300, canvas.height/2, 0, 200, 0, 100, 20, "white", 250);
}

function draw() {
  background(0);
  
  
  time2 = performance.now();
  timePassed = speedup*(time2 - time1)/1000;
  time1 = time2;
  
  let dx = Moon.XPosition - Earth.XPosition;
  let dy = Moon.YPosition - Earth.YPosition;
  let distance = sqrt(dx**2 + dy**2);
  let force = G*Earth.mass*Moon.mass/(distance**2);
  let angle = atan2(dy, dx);
  
  if(force>300000){
    force = 300000;
  }
  
  Earth.XAcceleration = force*cos(angle) / Earth.mass;
  Earth.YAcceleration = force*sin(angle) / Earth.mass;
  Moon.XAcceleration = -force*cos(angle) / Moon.mass;
  Moon.YAcceleration = -force*sin(angle) / Moon.mass;
  
  
  fill(Earth.colour);
  circle(Earth.XPosition, Earth.YPosition, Earth.size);
  Earth.XVelocity += Earth.XAcceleration*timePassed;
  Earth.YVelocity += Earth.YAcceleration*timePassed;
  Earth.XPosition += Earth.XVelocity*timePassed;
  Earth.YPosition += Earth.YVelocity*timePassed;
  
  fill(Moon.colour);
  circle(Moon.XPosition, Moon.YPosition, Moon.size);
  Moon.XVelocity += Moon.XAcceleration*timePassed;
  Moon.YVelocity += Moon.YAcceleration*timePassed;
  Moon.XPosition += Moon.XVelocity*timePassed;
  Moon.YPosition += Moon.YVelocity*timePassed;
}
```