# Interacting with 3D objects
	In this tutorial, we will demonstrate how to interact with 3D objects by touching, grabbing and throwing 3D balls.

## Objectives
- Learn how to interact with 3D objects.

## Main steps of the example
### 1 Creating a basic scene
 	Create the objects shown in the following image in the scene.
![](https://raw.githubusercontent.com/Ximmerse/Rhino-X/gh-pages/en/images/ballBasicScenes_config_1.png)
>AR Camera：Connect AR device camera. TrackingProfile must be added to it.   
![](https://raw.githubusercontent.com/Ximmerse/Rhino-X/gh-pages/en/images/ballBasicScenes_config_2.png)   
>Ground Plane：It is used to unify the coordinates of the virtual and real world.There can be multiple Ground Planes in a scene.      
>RxPlayerHand： Connect AR device controller.It can emit rays to interact with 3D objects in the scene.The property called Raycast Culling Mask must contain all levels of 3D objects that can be interacted with.In this tutorial, the property is set to UI and 3D Object.   
![](https://raw.githubusercontent.com/Ximmerse/Rhino-X/gh-pages/en/images/ballBasicScenes_config_3.png)    
>Plane：Add a Box Colider to it and the size of the collider must be the same as its.        
>RxEventSystem：To handle events produced by RxPlayerHand.      

### 2 Creating a 3D ball
![](https://raw.githubusercontent.com/Ximmerse/Rhino-X/gh-pages/en/images/ballBasicScenes_config_4.png) 

 - Set the level of the 3D ball to 3D Object   
 - Add a Sphere Collider component to the ball (the collider should be the same size as the ball)

### 3 Achieving touching effect
![](https://raw.githubusercontent.com/Ximmerse/Rhino-X/gh-pages/en/images/ballBasicScenes_config_5.png)      

- Add an OutLine component to the ball. It can make the edges of the ball show other colors.      
- Add a Touchable component to the ball. It allows the ball to be touched by rays.   
- Add an OutLineOnTouch component to the ball. When rays touch the ball, this component will trigger the outLine component effect.   
    
<img src="https://raw.githubusercontent.com/Ximmerse/Rhino-X/gh-pages/en/images/outline.gif" height="400px" width="450px" align=middle/>
### 4 Achieving grabbing effect
![](https://raw.githubusercontent.com/Ximmerse/Rhino-X/gh-pages/en/images/ballBasicScenes_config_6.png) 


- Add a Grabable component to the ball. After the ball is touched, users can press the controller button to grab the ball through this component.    

<img src="https://raw.githubusercontent.com/Ximmerse/Rhino-X/gh-pages/en/images/grabable.gif" height="400px" width="450px" div align=center  />
### 5 Achieving throwing effect

![](https://raw.githubusercontent.com/Ximmerse/Rhino-X/gh-pages/en/images/ballBasicScenes_config_7.png) 

- Add a Throwable component to the ball. After the ball is grabbed, users can press the controller button to throw the ball through this component.    
 
<img src="https://raw.githubusercontent.com/Ximmerse/Rhino-X/gh-pages/en/images/throwable.gif" height="400px" width="450px"/>

### 6 Resetting
- Add a canvas to the scene and create a button as the child of canvas.
- Add a Box Colider2D component to the button and set the colider to be the same size as the button.

 ![](https://raw.githubusercontent.com/Ximmerse/Rhino-X/gh-pages/en/images/ballBasicScenes_config_8.png) 

- Add a click event to the button and the event code is as follows.    

        using System.Collections;
    	using System.Collections.Generic;
    	using UnityEngine;
    	public class RestartButton : MonoBehaviour
		{
   			public GameObject SphereObject;
    		Vector3 SphereStartPos;
    		Quaternion SphereStartRos;

    		void Start()
    		{
        	SphereStartPos = SphereObject.GetComponent<Transform>().position;
        	SphereStartRos = SphereObject.GetComponent<Transform>().rotation;
    		}
    		public async void restartPosition()
    		{
        		SphereObject.GetComponent<Transform>().rotation = SphereStartRos;
        		SphereObject.GetComponent<Transform>().position = SphereStartPos;

        		//Reset physical engine
        		Rigidbody rigidbodySpere = SphereObject.GetComponent<Rigidbody>();
        		rigidbodySpere.Sleep();
        		await System.Threading.Tasks.Task.Delay(100);
        		rigidbodySpere.WakeUp();
    		}
		}


 
<img src="https://raw.githubusercontent.com/Ximmerse/Rhino-X/gh-pages/en/images/reset.gif" height="400px" width="450px"/>
##Note
1. Add the trackingProfile file to AR camera.
2. The property of RxPlayerHand called Raycast Culling Mask must contain all levels of 3D objects that can be interacted with.
3. Both 3D objects and UI need to add a collider. Rxplayerhand interacts with 3D objects through the collider.
4. The collider of UI and 3D objects should be consistent with their own size。