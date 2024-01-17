These libraries are required to run the project:
opencv-python
opencv-contrib-python

Please install them before running them.

Configuration
```
usage: Vehicle_Counting.py [-h] [--iscam] [--droi DROI] [--showdroi]
                           [--mcdf MCDF] [--mctf MCTF] [--di DI]
                           [--detector DETECTOR] [--tracker TRACKER]
                           [--record] [--headless] [--clposition CLPOSITION]
                           video

positional arguments:
  video                 relative/absolute path to video or camera input of
                        traffic scene

optional arguments:
  -h, --help            show this help message and exit
  --iscam               specify if video capture is from a camera
  --droi DROI           specify a detection region of interest (ROI) i.e a set
                        of vertices that represent the area (polygon) where
                        you want detections to be made (format:
                        1,2|3,4|5,6|7,8|9,10 default: 0,0|frame_width,0|frame_
                        width,frame_height|0,frame_height [i.e the whole video
                        frame])
  --showdroi            display/overlay the detection roi on the video
  --mcdf MCDF           maximum consecutive detection failures i.e number of
                        detection failures before it's concluded that an
                        object is no longer in the frame
  --mctf MCTF           maximum consecutive tracking failures i.e number of
                        tracking failures before the tracker concludes the
                        tracked object has left the frame
  --di DI               detection interval i.e number of frames before
                        detection is carried out again (in order to find new
                        vehicles and update the trackers of old ones)
  --detector DETECTOR   select a model/algorithm to use for vehicle detection
                        (options: yolo, haarc, bgsub, ssd | default: yolo)
  --tracker TRACKER     select a model/algorithm to use for vehicle tracking
                        (options: csrt, kcf, camshift | default: kcf)
  --record              record video and vehicle count logs
  --headless            run VCS without UI display
  --clposition CLPOSITION
                        position of counting line (options: top, bottom, left,
                        right | default: bottom)
```

I have trained the yolo darknet model to detect autorickshaws as well.
The model is used to detect all kinds of vehicles like trucks cars bikes autorickshaws tempos that are usually seen on the road. 

The project can be run as:
python3 Vehicle_Counting.py "./videos/1.MOV" --clposition "top"

I have changed the position of top to be aligned in the centre of the screen as that is the most useful case I came across.

There are multiple videos in the "video" folder. Some of these are videos that I came across. 
I also went out on the streets and captured videos through my camera through various angles and positions.

All of these are included in the "video" folder.


With camera input:

python3 Vehicle_Counting.py 1 --iscam



The traffic violation system can be considered to be comprised of three parts:
1. Detector
2. Tracker
3. Counter

The detector identifies the vehicle.
The trackers uses the bounding box of the detector to track the vehicle in the next frame.
There is a line running across the screen.
This can be considered as the white line ahead of a zebra crossing.
If the vehicle crosses this boundary while the signal is red, the image of the violator is saved in the folder as the region of interest 'roi.jpg'. 
With a good camera with high resolution, this system can be used to automate the entire process of detecting traffic violators.

Note:
while the program is running, you can press the 's' key to save screenshot of the video in the 'screenshots' folder.
