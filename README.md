# U2Eyes
## Description ##

We have created a software U2Eyes based on the original project [UnityEyes](https://www.cl.cam.ac.uk/research/rainbow/projects/unityeyes/ "UnityEyes"). U2Eyes generates synthetic binocular images intended for eye tracking and gaze estimation purposes which include essential eyeball physiology elements and model binocular vision dynamics. The software exports images with annotation such as head pose, gaze direction information, or 2D and 3D landmarks of both eyes amongst others.

The software may receive as input a series of configuration files (in xml format) to automatize the generation of a database:
  *	A user is identified (userid.xml file) by a different face shape (PCA model offered by UnityEyes), skin-textures, eye-textures, iris size, kappa angles, amongst other parameters.
  *	The head pose (headpose.xml) is a combination between head center spatial location (x, y, z coordinates) and face orientation (yaw, roll and pitch angles). It also defines the position of the point the user is looking at.
  *	The scene (scene.xml) which contains information about light color/direction/intensity and exposure/rotation of the scene (18 different scene models available).
  *	The camera (camera.xml) which defines intrinsic parameters of the camera as well as the final resolution of the image.

The software will also generate a series of output files:
  *	The generated image (in png format) with the resolution indicated in "camera.xml"
  *	The point of interests (poi_data.xml) containing the whole information about 2D/3D landmarks of eyelids, iris and pupil contour points and centers, caruncle and eye corners.
  *	All the above-mentionned input files (default ones in case these are not passed as argument)

## References ##
• Sonia Porta, Benoît Bossavit, Rafael Cabeza, Andoni Larumbe-Bergera, Gonzalo Garde, Arantxa Villanueva, U2Eyes: a binocular dataset for eye tracking and gaze estimation. 2019 OpenEDS Workshop: Eye Tracking for VR and AR. International Conference on Computer Vision (ICCV ’19). Seoul, Korea

## License ##
This project is licensed under a Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. 

Should you use this software in scientific publication, please cite the aforementioned papers.

## How to use ##
The main file is: SynthesEyesServer.cs

Execution with command line:
- /i = draw Point of Interest images
- /c + path to camera.xml
- /e + path to scene.xml
- /h + path to headpose.xml
- /u + path to userid.xml

In the app press key:
- 'g' to randomize gaze
- 'e' to randomize lighting
- 'h' to randomize headpose
- 'u' to randomize face
- 's' to export images


##  U2Eyes.exe
You can download an installed version of the software (U2EyesApp.zip) (https://drive.google.com/file/d/1XOejS_IYJbtiqz74rQcl-v7Zg3C4WJo4/view?usp=sharing), so you don't have to install Unity and compile the software.

Once you have unzipped the file, execute U2Eyes.exe file, it will generate a random example (image + configuration files) in the output folder.

You can use and modify these files to pass them as arguments to the software in order to generate customised conditions:

open cmd
go to U2EyesApp folder
write:
U2Eyes.exe /i /u "FULLPATHTO/userid.xml" /c""FULLPATHTO/camera.xml" /e "FULLPATHTO/scene.xml" /h "FULLPATHTO/headpose.xml"

U2Eyes.exe /c config/camera4k.xml /e config/scene.xml /h config/many_headpose.xml /u config/userid.xml

## Image generation for head-mounted eye-tracking devices
Mainly the HeadposeDef information is defined


```
import random

print("""<?xml version="1.0" encoding="utf-8"?>
<Headposes xmlns:xsd="http://www.w3.org/2001/XMLSchema"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Headpose>""")

for i in range(30):
        print("""      <HeadposeDef>
         <Rotation><x>0</x><y>0</y><z>0</z></Rotation>
         <Position><x>0</x><y>4</y><z>25</z></Position>
         <LookAtPoint>
            <x>"""+str(random.randint(-5,5))+"""</x>
            <y>"""+str(random.randint(-5,5))+"""</y>
            <z>0</z>
         </LookAtPoint>
      </HeadposeDef>""")
           
            
print("""   </Headpose>
</Headposes>""")

```
