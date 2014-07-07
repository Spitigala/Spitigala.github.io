---
layout: post
title:  "Racing With Javascript - Part 1"
date:   2014-07-08
categories: javascript oojs
---

![yoshi vd Diddy Kong](/img/yoshi.jpg)

I love racing games, and of course I love the entire Fast and the Furious movie franchise. I've always wanted to make my own game, but I'm not a game developer. So when I learned how to build one that works right in the browser at [Dev Bootcamp][devbootcamp] using a bit of Javascript, the race was ON! 

In this post, I'm going to teach you how to build your own javascript racing game. At the risk of putting advanced programmers to sleep, but with the goal of making beginners happy, I tried to make this tutorial as detailed as possible. But regardless of your skill level, I would definitely take a crack at it. Beating your friends in a race between Diddy Kong and Yoshi is totally worth it!

There are no fancy graphics and game engines involved. For version 1, this will be a strictly browser-based game. This means there's no database and we won't be keeping track of winners. That feature will be added in a follow-up post. We will also take a slightly Object-Oriented approach to creating the game and try to reduce dependencies along the way. This is very important when writing code that is modular and easily extensible. Of course, my code from this project can always be improved, so feel free to tear it apart and make it better.


The source code can be found [Here][js-racer-github].

Clone down the repo for the finished game. For help with cloning a repo, check out [this post][clone]. If you would like to follow along and build the game from scratch, delete all the javascript files and the racer.html file.


**STEP 1**

First, we're going to write the HTML code that will serve as a frame for our gameboard. Create a file called racer.html, and set up the structure as follows:

{% highlight html %}
<!DOCTYPE HTML >
<html>
  <head>
    <link rel="stylesheet" href="normalize.css">
    <link rel="stylesheet" href="race.css">
    <script src="http://code.jquery.com/jquery-1.11.0.min.js"></script>
    <script src="initialize.js" type="text/javascript"></script>
    <script src="prepare_game.js" type="text/javascript"></script>
    <script src="start_game.js" type="text/javascript"></script>
    <title>Javascript Racer</title>
  </head>
  <body>
    <h2>The Fast and the Delirious</h2>
    <h4>Press "A" to advance player1. Press "L" to advance player2.</h4>
    <table class="racer_table">
      <tr id="player1_strip">
        <td class="active"></td>
      </tr>
      <tr id="player2_strip">
        <td class="active"></td>
      </tr>
    </table>
  <body>
</html>
{% endhighlight %}

The "active" class will be used to show which cell the player is on as they advances through the race track. How do we display Diddy Kong and Yoshi? Take a look at lines 21 and 29 in the race.css file where we set the background images of our active cells to be the characters' images.


**STEP 2**

Let's create a file called initialize.js to kick off our javascript. Inside this file, let's tell our browser to do something when all the elements are loaded. We're simply going to call ONE function named prepareGame() that's going to tell our game to prepare itself to be played.

{% highlight javascript %}
	$(document).ready(function() {
    prepareGame();
});
{% endhighlight %}


**STEP 3**

The previous function prepareGame() doesn't do anything by itself. Let's create another file called prepare_game.js. In this file, we're going to add a bit more code. Let's write out the prepareGame() function and tell it what to do.

{% highlight javascript %}

function prepareGame() {
    var cellCount = 20
    var board = new drawBoard(cell_count);
    var player1 = new Player('Player1');
    var player2 = new Player('Player2');
    startGame(cell_count, player1, player2);
}

{% endhighlight %}


Here, we're first defining a cellCount variable and setting its value to 20. This is the number of cells our game board will contain. Our players will have to advance through all 20 to reach the end. We can easily change the number of cells by changing the variable's value.

Next, we create a new board by calling new on the constructor function drawBoard(). We also pass in the cellCount variable that we defined right before it. We want this function to create our game board with that many cells. We'll write out the code to actually creates the board in STEP 4.

We also create 2 players using the Player() constructor function, and pass in a name for each player (in this case, "Player1" and "Player2"). You can use any names you wish. We'll write out the code for the Player function in STEP 5.

Think of constructor functions as blueprints which you can use to build copies from, and give them unique properties such as the different player names. 

Finally we take the 3 new objects we created and pass them as arguments to a function called startGame(). This function will be responsible for allowing users to actually play the game. We will write the code for startGame() in STEP 6.

**STEP 4**

Let's write our code for drawBoard(). This function should create our game board and display it in our browser. We're going to use a mix of plain javascript and JQuery. 


{% highlight javascript %}

function drawBoard(cell_count) {
    for(cell=0; cell < cell_count; cell++) {
        $('.active').after('<td></td>');
    };
}

{% endhighlight %}


Our drawBoard() function takes in an argument of cell_count which was defined in our previous prepareGame() function. So what are the 3 arguments in our for loop?


- *cell=0* - This is our counter called cell, and it is initially set to 0.

- *cell < cell_count* - This is our condition. We want our loop do do something while this condition is true. Our incrementor below should keep increasing the value of "cell" while it is less than than the value of cell_count (in this case, 20).

- *cell++* - This is our incrementor. It will increase the value of "cell" by 1 as long as the above condition is true.

Then we have the following bit of JQuery.

{% highlight javascript %}
$('.active').after('<td></td>');
{% endhighlight %}

This will look in our racer.html file for an HTML element with the class name "active", and append a <td> element after it. Since we put this in our for loop, it will do this 20 times, creating a game board with 20 cells.

**STEP 5**

Now, let's write our Player function.

{% highlight javascript %}

function Player(player_name) {
    this.player_name = player_name;
    this.position = 0
}

{% endhighlight %}


When we create a new instance of Player, it will take a name as an argument and create a player with that name as a property. It will also give each player a default position of 0. This is the position our players will be in when they start the game. We'll need this value later.

Now that we have written out all the functions that create our board and players, let's move on to our startGame() function.

**STEP 6**

We'll start by creating a new file called start_game.js. In this file, let's add the following code to declare our function. It will take 3 objects as arguments: a cell count, and 2 players.


{% highlight javascript %}

function startGame (cell_count, player1, player2) {
	
}
{% endhighlight %}

**STEP 7**

Within the startGame() function, let's add 2 variables that will keep track of our players' positions. It will initially be set to the default position. Remember how we gave our players a position of "0" in the Player constructor function in STEP 5? We can access those values by writing Player1.position and Player2.position.

{% highlight javascript %}

	var player1_position = player1.position;
var player2_position = player2.position;

{% endhighlight %}


**STEP 8** 

After that, we will add a function called updatePlayerPosition() to update our players' positions as they advance through the board. This will take 2 arguments: the player number and that player's current position. We use JQuery to first remove the "active" class from the cell the player is currently in, and add it to the new cell, causing Diddy Kong and Yoshi to be displayed within their new "active" cells.

{% highlight javascript %}

function updatePlayerPosition(player_number, position){
    $("#player"+player_number+"_strip td").removeClass();
    $("#player"+player_number+"_strip td").eq(position).addClass("active");
};

{% endhighlight %}


**STEP 9**


We need to allow our players to control the game and advance their characters. For that we will make use of the Javascript keyup() function which gets called when a key is released. We will also set a variable called "keycode" to identify exactly which key was released. Add the following code below the updatePlayerPosition() function.


{% highlight javascript %}

$("body").keyup(function(e){
    var keycode = (e.keyCode ? event.keyCode : event.which);
});

{% endhighlight %}


**STEP 10**

Now let's add some logic to update our players' positions depending on which key is pressed. We want to use the "A" key to advance player1, and the "L" key to advance player2. The keyCode for "A" is 65 and "L" is 76. You can use any 2 keys you wish, and get their keyCode values from [here][keycode] 

Below we use two if-statements to say that if the "A" key is released, advance player1 by 1 position, and if the "L" key is released , advance player2 by 1 position. 

{% highlight javascript %}

$("body").keyup(function(e){
    var keycode = (e.keyCode ? event.keyCode : event.which);

    if (keycode == 65 && player1_position < cell_count) {
        player1_position += 1;
        updatePlayerPosition(1, player1_position);
    }

    if (keycode == 76 && player2_position < cell_count) {
        player2_position += 1;
        updatePlayerPosition(2, player2_position);
    }
});
{% endhighlight %}


**STEP 11**

Next, let's alert our players to let them know who won the game! We add 2 more if-statements that say if player1's position is equivalent to the cell_count (in our case 20, which should be the last cell on our board), create a pop-up alert stating that player1 has won. If player 2 reaches the 20th cell, create an alert stating that player2 has won the game. 


{% highlight javascript %}

$("body").keyup(function(e){
    var keycode = (e.keyCode ? event.keyCode : event.which);

    if (keycode == 65 && player1_position < cell_count) {
        player1_position += 1;
        updatePlayerPosition(1, player1_position);
    }

    if (keycode == 76 && player2_position < cell_count) {
        player2_position += 1;
        updatePlayerPosition(2, player2_position);
    }

    if (player1_position == cell_count) {
        alert(player1.player_name + ' wins');
    }
        
    if (player2_position == cell_count) {
        alert(Player2.player_name + ' wins');
    }
});
{% endhighlight %}


Our final Javascript within start_game.js should look like this:


{% highlight javascript %}

function startGame (cell_count, player1, player2) {

    var player1_position = player1.position;
    var player2_position = player2.position;

    function updatePlayerPosition(player_number, position){
        $("#player"+player_number+"_strip td").removeClass();
        $("#player"+player_number+"_strip td").eq(position).addClass("active");
    };

    $("body").keyup(function(e){
        var keycode = (e.keyCode ? event.keyCode : event.which);

        if (keycode == 65 && player1_position < cell_count) {
            player1_position += 1;
            updatePlayerPosition(1, player1_position);
        }

        if (keycode == 76 && player2_position < cell_count) {
            player2_position += 1;
            updatePlayerPosition(2, player2_position);
        }

        if (player1_position == cell_count) {
            alert(player1.player_name + ' wins');
        }
	        
        if (player2_position == cell_count) {
            alert(Player2.player_name + ' wins');
        }
    });
}


{% endhighlight %}


THAT'S IT! Our game is now ready to play. But tinker around with the code and add your own twist to it. Change the game's characters, add a background to the board, and maybe even add more than 2 players??

I will cover how to add a backend score-keeping system to this game in a future post. But for now, grab the nearest person for some feisty competition!




[js-racer-github]: https://github.com/Spitigala/javascript-racer
[keycode]: http://help.adobe.com/en_US/AS2LCR/Flash_10.0/help.html?content=00000520.html 
[devbootcamp]: http://devbootcamp.com/
[clone]: http://stackoverflow.com/questions/651038/how-do-you-clone-a-git-repository-into-a-specific-folder
