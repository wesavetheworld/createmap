Create Map
==========

Create Map converts a video to a map of the background shown in the video. It works best in videos where the camera movement is orthogonal to the camera direction. It works great, for example, in videos of 2d videogames.

For example, Create Map takes the frames of a video like this http://www.youtube.com/watch?v=Aw3AwK74wWQ as input, and then it generates the following background map:

![example](examples/example-mario-small.jpg)

([higher res](examples/example-mario.jpg))



Requirements:
-------------

- python
- python imaging library (PIL)
- ffmep or similar program for frames extraction

How to use createmap:
---------------------


If you want to create a map from a video:

1) use ffmpeg to extract the video frames:

ffmpeg -i video.mpg image%d.jpg

works with mpg, flv, mov, and most video formats. You can remove some of the initial and final frames
before starting map processing.

2) then change the settings in config.py. An easy way to do the following is:

keep

colorTolerance=50

does your image have borders? how big are them? modify:

imageBorders=(16,0,16,0)

so that the first number tells how big is the left border, the second number tells
how big is the top border, then the right and the bottom border. If the image contains
no borders, use (0,0,0,0) or something like (1,1,1,1) or (2,2,2,2) if you just worry
about a small border in the whole image.

3) how does your video move? if it moves only from left to right (at any times moving to left,
or right, but never top or down), use:

checkRange=(10,0,10,0)

if it produces a bad map because there is too much movement, try bigger values like:

checkRange=(20,0,20,0)

a way to know if that's the problem is to check the logged offset values to see if they are
near the limits or not.

If the video moves only from up to down (never left or right), use:

checkRange=(0,10,0,10)

or:

checkRange=(0,20,0,20)

If the video moves in all directions, you'll have to set it like this:

checkRange=(10,10,10,10)

or

checkRange=(20,20,20,20)

but it's going to be many times slower than if it only moves in one-axis. If it moves very slowly,
perhaps you can try with this setting first:

checkRange=(5,5,5,5)

4) Now you can run the map creator, just use:

python createmap.py framedir results.jpg

where framedir is the path to the frames directory.




