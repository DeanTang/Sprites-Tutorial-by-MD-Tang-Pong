<h1>Sprites Tutorial</h1>
Although our program is compiling, the code isn't optimised. What if we want to display multiple characters using different images? How much code do we need to duplicate for this task?
<br>
There are multiple ways we could make our code writing more efficient. For instance, we could use Object Oriented Programming, however for the course of this tutorial we will be using structs and enums instead.
<br>
<h2>Let's format our code properly</h2>
Since our program is using the concept of heroes, we can create a data structure about heroes.
The data structure will consist of only a sprite for now. We will add more attributes as we progress.
So the code for the data structure should look a bit like this:
<br>
<pre>
<code>
struct hero_data 
{
	//Sprite used for the hero
    sprite h_sprite;
};
</code>
</pre>
<br>
Moreover, we would like to ensure that all elements that are loaded into the memory, are written
at the same place in our code. To do this we put every load procedures in the same function, let's call
it <code>load_resources()</code>: 
<pre>
<code>
void load_resources()
{
	//Load mage.png
    load_bitmap("mage","mage.png");
}
</code>
</pre>
<br>
While it might seems that we are adding codes unnecessarily, all the changes we are making now will help
us make the expansion of our program much easy and more organised (and therefore, easier to debug).
<br>
Now our task is to create a function where we can make our hero which includes assign its sprites and coordinates.
<br>
<pre>
<code>
hero_data new_hero()
{

    hero_data result;
	
	//Get the image of the sprite
	bitmap default_image = bitmap_named("mage");
	
	//Create sprite from the image
    result.h_sprite = create_sprite(default_image);
	
	//Set the coordinates
    sprite_set_x(result.h_sprite,350);
    sprite_set_y(result.h_sprite,250);
	
    return result;
	
}
</code>
</pre>
<br>
Finally, all we are left to do is to create a function to draw the sprite.
<br>
<pre>
<code>
void draw_hero(const hero_data &hero)
{
    //Draw the hero_sprite
    draw_sprite(hero.h_sprite);
}
</code>
</pre>
<br>
Alright, since we have now a better formatted code, let's make our program more interactive.
<br>
<a href="HandleInput.md">NEXT</a>