<h1>Sprites Tutorial</h1>

<h2>Sprite Layers and handle inputs</h2>

In section, we will learn how to use layers with sprites, which will allow us to change the image of our sprite at run-time.
<br>
Let's start by adding a job system which will help us determine which bitmap to be used.
<br>
<pre>
<code>
enum job
{
    WARRIOR,
    TANK,
    MAGE,
    CLERIC
};
</code>
</pre>
<br>
To represent each of the following "jobs", we will be using the following images, feel free to download them and place them 
inside the <code>/resources/images</code> directory.
<br>
<table>
<tr>
<img src="https://i.imgur.com/ahtN42u.gif">
</tr>
<tr>
<img src="https://i.imgur.com/99gqIzb.gif">
</tr>
<tr>
<img src="https://i.imgur.com/fIH2arn.gif">
</tr>
<tr>
<img src="https://i.imgur.com/xaTaAnN.gif">
</tr>
</table>
<br>
Inside the <code>load_resources()</code>, load all the images into the memory.
<br>
<pre>
<code>
void load_resources()
{
    //Load all images
    load_bitmap("warrior","warrior.png");
    load_bitmap("tank","fighter.png");
    load_bitmap("mage","mage.png");
    load_bitmap("cleric","cleric.png");
}
</code>
</pre>
<br>
In order to associate a job with a specific bitmap, we will use the following function that returns the associated bitmap 
based on the job.
<br>
<pre>
<code>
bitmap hero_bitmap(job hero_job)
{
    //Return bitmap based on job
    switch(hero_job)
    {
        case WARRIOR: 
            return bitmap_named("warrior");
        case TANK:
            return bitmap_named("tank");
        case MAGE:
            return bitmap_named("mage");
        case CLERIC:
            return bitmap_named("cleric");
    }
}
</code>
</pre>
<br>
In the <code>new_hero()</code> function, we will add layers to our sprite consisting of our new images. We will hide all of 
them except the default one at start. Note: The new procedures used here are <code>sprite_add_layer</code> and <code>sprite_hide_layer</code>.
<br>
<pre>
<code>
hero_data new_hero()
{
    hero_data result;

    //Get the image of the sprite
    bitmap default_image = hero_bitmap(WARRIOR);

    //Create sprite from the image
    result.h_sprite = create_sprite(default_image);

    //Add layers to the sprite with appropriate names
    sprite_add_layer(result.h_sprite, hero_bitmap(TANK), "TANK");
    sprite_add_layer(result.h_sprite, hero_bitmap(MAGE), "MAGE");
    sprite_add_layer(result.h_sprite, hero_bitmap(CLERIC), "CLERIC");

    //Hide all except the first one (index 0)
    sprite_hide_layer(result.h_sprite, 1);
    sprite_hide_layer(result.h_sprite, 2);
    sprite_hide_layer(result.h_sprite, 3);

    //Set the coordinates
    sprite_set_x(result.h_sprite,350);
    sprite_set_y(result.h_sprite,250);

    return result;
}
</code>
</pre>
<br>
Now, to be able to switch between jobs, we will create a new procedure that will switch between the current job and the new job.
<br>
<pre>
<code>
void switch_hero(hero_data &hero, job target)
{
    // only do this if there is a change
    if (hero.h_job != target)
    {
        // show then hide layers
        sprite_show_layer(hero.h_sprite, static_cast<int>(target));
        sprite_hide_layer(hero.h_sprite, static_cast<int>(hero.h_job));

        // remember what is currently shown
        hero.h_job = target;
    }
}
</code>
</pre>
<br>
Finally, we will allow the user to change between jobs through the number keys from 1 to 4.
<br>
<pre>
<code>
void handle_input(hero_data &hero)
{
    // Allow the player to switch ships
    if (key_typed(NUM_1_KEY))
        switch_hero(hero, WARRIOR);
    if (key_typed(NUM_2_KEY))
        switch_hero(hero, TANK);
    if (key_typed(NUM_3_KEY))
        switch_hero(hero, MAGE);
    if (key_typed(NUM_4_KEY))
        switch_hero(hero,CLERIC);

}
</code>
</pre>
<br>
Since our main program does not currently allow the user for input, it is time to change our main function.
For this, we will need a loop that repeats itself until the user quits the program and the instruction <code>process_events();</code>.
<br>
<pre>
<code>
int main()
{
    load_resources();

    hero_data hero = new_hero();

    open_window("Sprite Tutorial",800,600);
    clear_screen(COLOR_WHITE);

    //Main loop
    do
    {
        clear_screen(COLOR_WHITE);
        //Event handler
        process_events();

        draw_hero(hero);

        //Accepts input to change job
        handle_input(hero);

        update_hero(hero);

        refresh_screen(60);
    } while (!quit_requested());

    return 0;
}
</code>
</pre>
<br>
In case you got lost along the way, you can see the source <a href="https://drive.google.com/file/d/1hqwbnFPNhgwZ6vDEuwEPF_AQ_q8s2K7e/view?usp=sharing">here</a>.
<br>
<a>NEXT</a>