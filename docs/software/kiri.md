# Kiri:Moto BASICS 

**Kiri:Moto** is a unique browser-based slicer for 3D printing and a tool-path generator for CNC mills and laser cutters. It is completely free and open-source with a focus on privacy and ease-of-use. It is actively being developed and updated.

**Ease of use.**
The author of this document had not previously opened a CAM application,  His prior CNC experience was limited to tracing a “crown test” from the supplied gcode.   Therefore the following is both a testament to just how quickly one can get up and running with Kiri:Moto, and a warning that there may be other, better ways of implementing the software! 

**1) Language**
Open Kiri:Moto and choose your language from the  <img width="24" alt="icon" src="https://user-images.githubusercontent.com/122715389/212527813-029fa2c6-343b-4388-a970-3b310a695fd1.png">icon in the top right of your screen.

<img width="50%" alt="application preferences menu" src="https://user-images.githubusercontent.com/122715389/212527623-fb474ad6-00f8-4ca9-b1c7-b7d86e3b410d.png">

**2) Preferences Setup**. 
Open the Setup Menu (top of the left hand toolbar) and select “Prefs”.
The default setup should not need changing unless you have some specific requirements, but make sure that you have selected the correct workspace units for your purpose.
 
<img width="50%" alt="machine setup menu" src="https://user-images.githubusercontent.com/122715389/212527695-f2e25e65-6e3e-4632-ad10-d3f2ccbeb8c6.png">

**3) Machine Setup**
Open the Setup Menu and select “Machine”

Check that the “CNC” button is shaded then select any Standard Device (I used “any generic Gbrl” which seems to talk nicely in Marlin too),  and make the following changes:
 - Change the Name of the machine to whatever you fancy.
 - Enter the build volume of your machine.
 - Change the Max Spindle Length to match the longest spindle you will be using.
- In the **Output** menu check that the file extension is “gcode”.
- In the menu **Gcode Macros**, there is provision for insertion of special instructions for tool changes, and at the beginning and end of the project, but since this is day one, we’ll ignore those until a slightly further down this page.

<img width="50%" alt="image" src="https://user-images.githubusercontent.com/122715389/212537273-698fd9af-7abc-4f52-8e70-a4936a43e5d4.png">

**4) Setting up the Operation Modifiers (Right Hand Menu)**

Click on the **Limits** menu and change the following values: 
 - Z Thru to (say 1mm) - this is the amount your bit will travel into the spoil board in through cuts.
 - Z Clearance - 2mm - the amount your bit will lift above the work while travelling.   Changing the clearance plane to something a little smaller really speeds up a job since the z axis is the slowest. This is how far above the material it should travel to before it moves.
 - Z Feed -  this is the maximum Z travel rate in mm/minute, set it to 480.
 - XY feed - sets the maximum XY travel speed - (2100)

The **Output** menu is next.
 - Leaving **Conventional** unchecked will set milling direction at **climb cutting**. You should change the milling direction depending on what kind of material you are cutting. 
 - **Ease Down** will automatically ease linear cuts and spiral plunge cuts. 
 - **Depth First** optimises pocket cuts with depth priority.
Finally (for now) the **Origin** menu;

 - Setting the z-axis origin to the **top** of the material makes it easy to set the home position, along with that is program start – at ****origin**. 
<img width="100%" alt="white pagebreak strip" src="https://user-images.githubusercontent.com/122715389/212532745-e46d4bc1-947f-4830-95bd-846d8c1d265a.png">

**5)Tools**

Now we are ready to look at **TOOLS**.
There is a basic set of tools ready to be modified and there is absolutely no need to create a tool called “Sharpie” but it’s a nice exercise to help create an understanding of how the tool setup works.   Each tool to be used, requires a new setup so that the software can figure out what needs to be done.

<img width="50%" alt="tool setup menu" src="https://user-images.githubusercontent.com/122715389/212528359-85002433-def6-42ef-88a2-459d7db2371a.png">

Go back to the **Setup** menu on the left hand side of the screen, and click on **Tools**. NOTE - in a very rare instance of confusing menus, this is not the "tools: menu that you can see on the screen, it's the one you see when you click **Setup**.
Once you are there the menu is very intuitive, so use it to draw the tool of your choice - things will get a little more serious as you start to fill in the tools you actually have, but for now, why not just copy my Sharpie?

**CONSIDER YOURSELF READY TO GO!**
You are ready to generate some GCode. 
Let’s start with generating some 2D gcode, Good for pen plotting or 2D milling (cutting things out).
Download the [Crown Vector](https://www.v1engineering.com/wp-content/uploads/2018/08/0102.zip) drawing, and import the SVG file directly into Kiri:Moto.  Kiri:Moto will automatically convert the 2d drawing to a 3d object with a depth of 5mm so there's no need to fiddle with any other format.

<img width="50%" alt="Stock Modifier for Crown" src="https://user-images.githubusercontent.com/122715389/212528595-cb212c28-0fbb-4255-85ba-9a27d9931ea3.png">

Using your paper size as the “Stock” will make it easy to position the drawing, keep the height at 5mm because we have already set up Z0 to be on the top surface.

<img width="50%" alt="Scale Crown" src="https://user-images.githubusercontent.com/122715389/212528613-c9922d75-3a29-4c27-825f-7392bdb23de5.png">

If the drawing is too big for your taste, pop over to the **Tools** menu (this time the one that you can see on the right hand menu on-screen), select **Scale**, and resize it as you wish.

<img width="50%" alt="Milling Operations crown" src="https://user-images.githubusercontent.com/122715389/212528632-e17871df-1745-4635-9d4a-afcb43d9f8cd.png">

Now we are getting to the action part!  Go to the **milling operations** menu at the *bottom of the page* and click on the **+**.  From the popup, select **trace**.

<img width="50%" alt="trace operation setup" src="https://user-images.githubusercontent.com/122715389/212538060-1c161b86-e063-4127-acb9-838ab0fad1cf.png">

Set up the **trace** menu to look a bit like this:
 - **tool** - Sharpie
 - **select** “loops” because our edges are all closed loops
 - **type** “follow” for obvious reasons
 - **offset** “center”
 - **spindle rpm** - does not matter
 - **step down** - “0” will keep the tool on the surface
 - **cut thru** - 0 will just make sure!
 - **feed** and **plunge** rates are a bit arbitrary too, but lets see how 250 goes and let’s hope it doesn’t plunge at all or we'll ruin our sharpie!

<img width="50%" alt="trace crown" src="https://user-images.githubusercontent.com/122715389/212528881-14ded58e-f372-443e-b15f-311dec993deb.png">

Now click on the little **+**  sign in the bottom of the **trace** popup, you can move your cursor onto the edges you want to trace and click once - when selection is confirmed the trace will appear in red so it’s easy to spot whether anything has been missed.

<img width="50%" alt="preview crown" src="https://user-images.githubusercontent.com/122715389/212528903-487cfb64-b610-40b9-b92c-4f2077e28726.png">

It’s time to pop back up to the **start** menu and check on our handiwork.  Preview the tool travel path and even check out an animation although for this one, if the tool (Sharpie) is at Z0 there may not be any lines left so it could be a bit uninteresting!

If thngs work as expected you can export your first bit of gcode and run breathlessly to your waiting machine, where no doubt you’ve had the Sharpie set up for just this minute! 

<img width="50%" alt="export box" src="https://user-images.githubusercontent.com/122715389/212528940-08d6a9d2-8163-443d-b1d3-f1bb4caf4dec.png">

If you've worked out how to load the gcode into your machine and all went according to plan you should have something that looks a bit like this:

<img width="50%" alt="drawing crown" src="https://user-images.githubusercontent.com/122715389/212528979-2851b2fc-02fd-4d33-9ba7-1683d4da6113.png">

You are now one of the cool kids! 

### But wait… THERE’S MORE!

While you have Kiri:Moto open and your shiny new V-bit just busting to get dirty, let’s try a spot of engraving.  As always, it would be wise to practice on a bit of rigid foam before you start engraving notes on your mother’s best table because things can and probably will go wrong.

<img width="50%" alt="two trace operations" src="https://user-images.githubusercontent.com/122715389/212538599-a1bd7153-735f-41e7-8c11-1bbcdff10674.png">

Reopen the **Trace** menu and swap your Sharpie for your vee bit and, because you want to go a little below the surface this time enter 1mm as a **step** down and again as a **cut thru**.

For your first attempt at engraving foam, 1mm should be nicely visible.

Right now you want to hit “export” and get on with it, and it would be fine if you did but there’s ONE MORE THING you might like to try.

Go back and hit that **+** sign beside the **trace button**, and select *another* **trace** operation.

Set up the new tab exactly the same as the previous one, *except* for **offset**, select **outside**

<img width="50%" alt="trace crown circle" src="https://user-images.githubusercontent.com/122715389/212529334-75b2a8b5-14c4-4ebe-93a5-d0dcb731afd9.png">

Now hit the little **+** button in the pop-up and select the circle at the top of the crown.  (Technically it’s not quite a circle but that will do).

**Tick** it to save it all (or don't, because *mostly* it saves itself anyway) and scoot back to the **start** button and check out your handiwork in the preview panel.

<img width="50%" alt="preview crown" src="https://user-images.githubusercontent.com/122715389/212529337-dc6248a5-6a7e-468c-ab19-704396d8eeca.png">

Miraculously a separate ring has appeared around the circle exactly half the width of your v-bit away.

This is just an example of what can be done by tweaking parameters in what seem to be very simple tools.

If you wish to increase the offset dimension, just set up an imaginary tool that’s twice the width of the offset you want, and the machine will do the rest!

<img width="50%" alt="crown cross foam" src="https://user-images.githubusercontent.com/122715389/212529345-7c83c19c-defd-45a0-8349-04c28acb72a0.png">

I’m happy to call this a result.   The circle came out very nicely and the result held no surprises!  If I wanted to have a crown engraved in a bit of priceless ebony, I reckon I could do that now without changing anything.

<img width="50%" alt="crown engrave foam" src="https://user-images.githubusercontent.com/122715389/212529391-1ca4cd96-38c0-4a55-98af-0c36d0d582dd.png">

# AND NOW TO MAKE SOMETHING!

Actually that’s just a catchy headline, because playing in foam is oh so rewarding when things go right, and not terribly punishing when they don’t.

Here’s a V1 logo stolen from somewhere on this site which presents no real challenge but it will allow us to explore a few operation options. (The image isn’t at an angle, it’s just the sort of geometry that would make M C Escher proud.)

<img width="50%" alt="vi logo rough outline operation menu" src="https://user-images.githubusercontent.com/122715389/212530155-69366fea-a712-4227-aee9-cb07fa438031.png">

It’s really simple and given that it’s in foam probably doesn’t even need a “rough-in” stage, but never the less, check this out: Go to the **Milling Operations** (it's the one at the bottom of the page) tab and add a **rough** and **outline** operation.

If you poke around in those operation popup menus, you will see that you can vary the amount left in the rough in stage for a finishing pass, then let the outline do the rest.   For now though, since we are in exploring mode,  delete those two windows and we’ll start again taking a different, much more complicated tack.

Because we are going to cut this out of a piece of stock, we had better add some **tabs** to keep everything together once the outline is cut out.

<img width="50%" alt="vi logo tabs" src="https://user-images.githubusercontent.com/122715389/212530320-cbe4f8d7-dce2-4b00-ade0-f0288e56aece.png">

Go to the  **operations modifier** menu (on the right hand side) and click on the **tabs** item.

If your eyes will allow you to ignore another disconcertingly crooked-yet-not crooked image, set the tabs dimensions to taste (there’s a tool tip on every menu and these are no different), click the “+” sign and click on your model in the spots you want to place a tab.
Now let’s go back to the Operations Menu at the bottom of the page and over-complicate things in the interest of science.

<img width="50%" alt="v1 logo first pocket operator" src="https://user-images.githubusercontent.com/122715389/212530448-7fb80db1-5378-45b5-ae7e-c1655f5b0009.png">

Add *four* **pocket** operations and an **outline**.  Just for fun, I’ve decided to taper the edges of the letters V1, to make them a little finer, and to give us an excuse to set up a tool change.   At the beginning of this document I may have suggested leaving out the “tool change” code for a later time, which is a shame, because that time has arrived.

[<img width="50%" alt="tool change code" src="https://user-images.githubusercontent.com/122715389/212539631-7a94724f-1259-4ca7-b4ba-bde6fddb062c.png">](https://docs.v1engineering.com/tools/milling-basics/#gcode-start-tool-change-and-ending)

Race back to the **setup** menu, select **Device>gcode macros> tool change**,  and cut and paste the code that best suits your machine from the "Milling Basics page, see [GCode Starting Ending and Tool Change. ](https://docs.v1engineering.com/tools/milling-basics/#gcode-start-tool-change-and-ending)

This will tell the machine to pause and do whatever machines do while you fiddle with the tool change and to start again where it left off when you tell it to do so.
                                                                                                              
Curiously (or not) you can skip that bit if you download the gcode as a zipfile.  When you unbundle the file each operation will appear as a separately titled bit of code so you can manually simply start each in your own time.   The gcode link will give you all of the operations in one bundle of code.

<img width="50%" alt="output operation modifier menu" src="https://user-images.githubusercontent.com/122715389/212539248-2cf6d8c6-c4ef-49ca-804c-a9ab26037e4b.png">

While that’s sinking in, whizz back to the **Output** menu and check that the **Tool Init** box is checked, unless you have an automatic tool changer, in which case it should not be checked, but if you have a tool changer, you probably aren't reading this beginner's guide! 

With that done, let’s get back to our the operations menu at the bottom of the page
 
If we don’t change our mind about how we want things to work, we have the ability to select each area of the project as a separate operation, and rearrange the order of those operations simply by sliding the tabs on the bottom of the screen.   From the first image above, I have clicked the **+** button and added the face of the lettering as my first operation.  I’ve decided to use a V bit for that operation and am happy that it will cut within the outline of the letters.   I could have used the “Outline” operation for more options but this is fine.
  
<img width="50%" alt="FOUR operations" src="https://user-images.githubusercontent.com/122715389/212531364-1e3a4ca4-0081-4aea-80dd-0948ae234189.png">

Next, for demonstration purposes, I’ve decided I want the logo cut first, so again I’ve opened the next pocket operation and selected just the logo, and so on until the only thing left to do is cut the outline.  For this, quite logically I’ve selected the outline operation and checked “outside only” to ensure the machine doesn’t go over all the work already complete..

<img width="50%" alt="V1 logo cut in foam" src="https://user-images.githubusercontent.com/122715389/212536146-64c15e16-e337-4003-9e52-0bd9d1d1cf75.png">

All that’s left to do is to slice, preview and export, and it’s ready to go.


