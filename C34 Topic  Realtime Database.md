C34 Topic : Realtime Database 

* learn the importance of using realtime database to create multiplayer games 
* * learn how to connect, read and write data into a remote real time database. 
  * * Create a ball which moves synchronously in different browsers. 
  * * Create a remote real time database



STEPS: 

1. Designing a multiplayer game : The game is in different states in the two browsers. For a multi-player game, we need the two browsers to have the game at the same state at the same time. Everything in the two browsers should be synchronous. Currently the games are asynchronous and independent from each other. 

2. Write the code to create a simple ball which can move using arrow keys. 

```javascript
var ball;

function setup(){
    createCanvas(500,500);
    ball = createSprite(250,250,10,10);
    ball.shapeColor = "red";
}

function draw(){
    background("white");
    if(keyDown(LEFT_ARROW)){
        changePosition(-1,0);
    }
    else if(keyDown(RIGHT_ARROW)){
        changePosition(1,0);
    }
    else if(keyDown(UP_ARROW)){
        changePosition(0,-1);
    }
    else if(keyDown(DOWN_ARROW)){
        changePosition(0,+1);
    }
    drawSprites();
}

function changePosition(x,y){
    ball.x = ball.x + x;
    ball.y = ball.y + y;
}

```

3. Let's open the application in two different browsers. 

   Let's move the ball and see what happens. 

   * * What do you see? 
   * * The ball in the two browsers move independently. 
   * * Their movements are asynchronous



4. This happens because the ball's position in each browser is independent of the other's position. 
   * But what if we could store the ball's position in a remote common database and our application reads the ball's position from the database and updates it when it changes. 
   * * Database servers are computers which are remotely connected through internet and maintain your data which you can use in your applications. 
     * * The two browsers will read the position of the ball from the common remote database and they will always be synchronized. This is how multiplayer games work. 
       * * They store the position of the state of the game at all times in a remote database. All the players' console/browsers read the game from this remote database and write to it when they make any change in the game.
         *  Let's make a remote database for our simple application on the cloud internet. This remote database will store the state (positions) of the ball and will allow us to read or write to it at any time.
           5. * We will be using Google Firebase's Real Time Database for this purpose. 
              * * Create a Real Time Database and create a variable call ball which stores two values x and y. 
                * * The database can be compared to a JSON data structure format. 
                  * * ball = { x: 250, y: 250 }



6. how to get a reference to the position of the ball in the database? 
7. * .ref() is used to refer to the location of the database value we care about. 
   * * .on() creates a listener which keeps listening to the changes in the database. 
     * * Everytime a change in the database values of position (reference) happens, the readPosition function is called. 
       * * If there is any error in reading the values in the database, the showError function is called.