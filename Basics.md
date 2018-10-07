<h1>Sprites Tutorial</h1>
In video games, sprites provide an element of aesthetic and interaction. Although some games does not require any graphics <sup>[1]</sup>, using sprites can convey much more information than plain text
In this tutorial, we assume that the reader has basic understanding of concepts used in c++ such as arrays and structs, and has already made all necessary installations for splashkit.
<h2>Basics</h2>
In Splashkit, a sprite will consist essential of an image and the x-y coordinates.
The following line is used to declare a sprite.
<br>
<pre>
<code>sprite my_sprite;</code>
</pre>
<br>
<br>
For the creation of a sprite, we can make use of the <code>create_sprite</code> function,
in which we need to specify the name of the bitmap we are making use.
<br>
<pre>
<code>sprite create_sprite(const string &bitmap_name);</code>
</pre>
<br>
<br>
To load an image into the memory and give it a <code>bitmap_name</code>, we can make use of:
<br>
<pre>
<code>bitmap load_bitmap(string name, string filename);</code>
</pre>
<br>
<br>
To assign the coordinates, we need to use 2 different procedures for the x and y coordinates, which are:
<br>
<pre>
<code>void sprite_set_x(sprite s, float value);</code>
</pre>
<br>
<pre>
<code>void sprite_set_y(sprite s, float value);</code>
</pre>
<br>
<br>
To draw our sprite, we use the <code>draw_sprite</code> function:
<br>
<pre>
<code>void draw_sprite(sprite s);</code>
</pre>
<br>
<br>
<h3>Practice the basics</h3>
So, now our goal is to display a sprite on the screen using splashkit.
<br>
For this tutorial, we will create a directory called SpritesTutorial inside the <code>C:/msys64/home/your_username/</code> directory, which is the default location accessible using mysys mingw x64.
Inside we create our c++ project file, using the MSYS2 MINGW as shown below:
<figure>
<br> 
<img src ="https://i.imgur.com/fIH2arn.gif">
<figcaption>Figure 1: Creating the directory and resource folder</figcaption>
<br>
</figure>
<br>
Right-click on the following image and save it as "mage.png" into the directory: <code>C:/msys64/home/your_username/SpritesTutorial/Resources/images</code>.
<br>
<br> 
<img src ="https://i.imgur.com/7eQclse.png">
<figcaption>Figure 2: Our little buddy</figcaption>
<br>
So now, open the program.cpp file from the directory: <code>C:/msys64/home/your_username/</code> using the editor of your choice, for example: Visual Studio Code.
<br>
Inside the main, we want to load the image and give it a name. For this, we use the function <code>load_bitmap</code>:
<br>
<pre>
<code>load_bitmap("mage", "mage.png");</code>
</pre>
<br>
<br>
Next, let us create a window of resolution 800x600 with a white background.
<br>
<pre>
<code>open_window("Sprite Tutorial",800,600);</code>
</pre>
<br>
<pre>
<code>clear_screen(COLOR_WHITE);</code>
</pre>
<br>
<br>
Now is the time for us to create our sprite, but first we need to create a bitmap using the image that we have already loaded inside our memory.
<br>
<pre>
<code>bitmap hero_img = bitmap_named("mage");</code>
</pre>
<br>
<pre>
<code>sprite hero_sprite = create_sprite(hero_img);</code>
</pre>
<br>
<br>
Since we now have the image set for our sprite, all we are left to initialise are the coordinates. We will set the x-coordinate to 350 and the 
y-coordinate to 250.
<br>
<pre>
<code>sprite_set_x(hero_sprite,350);</code>
<br>
<code>sprite_set_y(hero_sprite,250);</code>
</pre>
<br>
<br>
The time has finally come for us to draw our sprites. And don't forget to update the screen, otherwise the image won't appear. We will set the 
target fps to 60. And to make sure that the window does not close immediately, we will add a delay of 2 seconds (2000 milliseconds).
<br>
<pre>
<code>draw_sprite(hero_sprite);</code>
<br>
<code>refresh_screen(60);</code>
<br>
<code>delay(2000);</code>
</pre>
<br>
<br>
If you did everything right, the output should look a bit like this:
<br>
<br> 
<img src ="https://i.imgur.com/2gL96V4.png">
<figcaption>Figure 3: Output</figcaption>
<br>
Did you get a similar output? Or, was it too confusing for you? Have a look at the code, <a href="https://drive.google.com/file/d/1VIU9L5gZLxXteXVmLOE7OrPFTpj6q5Za/view?usp=sharing">here</a>.
<br>
Although our program is compiling, the code isn't optimised. What if we want to display multiple characters using different images? How much code do we need to duplicate for this task?
<br>
There are multiple ways we could make our code writing more efficient. For instance, we could use Object Oriented Programming, however for the course of this tutorial we will be using structs and enums instead.
<br>
<h3>References</h3>
<br>
[1] 	M. Barton, "The History Of Zork," 28 06 2007. [Online]. Available: http://www.gamasutra.com/view/feature/1499/the_history_of_zork.php. [Accessed 08 10 2018].
<br>
<a href="UsingStructsAndEnums.md">NEXT</a>