---
title: "Tech"
date: 2024-04-01T00:17:58+08:00
lastmod: 2024-04-01T00:17:58+08:00
author: ["Chen"]
keywords: 
- 
categories: 
- 
tags: 
- tech
description: "University project"
weight:
slug: ""
draft: false # 是否为草稿
comments: true
reward: true # 打赏
mermaid: true #是否开启mermaid
showToc: true # 显示目录
TocOpen: true # 自动展开目录
hidemeta: false # 是否隐藏文章的元信息，如发布日期、作者等
disableShare: true # 底部不显示分享栏
showbreadcrumbs: true #顶部显示路径
cover:
    # image: "https://www.sulvblog.cn/posts/blog/how_to_write_a_blog/1.png" #图片路径例如：posts/tech/123/123.png
    # image: "/posts/tech/tech1/1.png"
    # image: "https://upload.wikimedia.org/wikipedia/commons/7/73/Pale_Blue_Dot.png"

    image: "https://www.qualcomm.com/content/dam/qcomm-martech/dm-assets/images/device/image/Meta-Quest-2-Transparent.png"
    
    # image: "img/1.png"
    caption: "" #图片底部描述
    alt: ""
    relative: false
---
<!-- this is test -->
<!-- ![example image](/posts/tech/tech1/1.png) -->

<!-- ![example image](https://www.qualcomm.com/content/dam/qcomm-martech/dm-assets/images/device/image/Meta-Quest-2-Transparent.png) -->

# Background/Motivation
I have attended the kickoff course of IVAR in 2022. It was the most interesting lecture I have ever attended. But I didn't have any experience about unity at that time so I was thinking I could attend this course next year after I got some experience with unity. However, I still didn't try to learn unity. So here I am. There are two purposes of taking this course: 
1. following the course schedule sysmatically to finish a project 
2. find an interesting topic for my master thesis. 

The goal of the course is to create locomotion technique and implement interaction task in a parkour map in XR environment with meta quest.

# The Idea
After the first lecture every attendee was required to write a short motivation email to the tutor. Because the number of equiments is limited, the number of students who can attend this lecture is also limited. 

I was thinking about all the different sports I have tried before, such as bouldering, rowing, shooting. But later I decided to implement skateboarding experience. The reasons are as follows: 
1. the people without skateboarding experience before can try to skateboard as well. 
2. people get no physical injuries 

I don't need to do any change to parkour.

# Progress
## Learn one tutorial
At the beginning of the class, everyone was offered a tutorial link, which could be relavent to our topic. I picked a tutorial about bouldering at the beginning. But later I switched to skateboarding so I could not use the experience from this tutorial.


## First Unity Project - Animal collecting coins
Two month after first lecture I followed one tutorial on Youtube([Bird collect coins](https://www.youtube.com/watch?v=EZxdMyFbJcI&list=PLZ1b66Z1KFKiGehDxoWXh3oHA24iT5ZCr)) to build my first unity project.

## Run the parkour/Set up VR
Github link([parkour](https://github.com/wenjietseng/VR-locomotion-parkour/tree/main)) 
## Troubles
I met following new bee problems at the very beginning of my project.
* Mac can not load. It has to be windows system. 
* The cabel of meta quest is short. 
* How to fine tuning the rotation of the skateboard. 
* What interaction movement can I think for t-shape task?
* The movement on the slope

# Code

retrieves the horizontal input from the primary thumbstick and assigns this input to the variable steerAngle, which is used to control the rotation of the skateboard.

determines how fast the skateboard rotates in response to the thumbstick input.

```
    float steerAngle = OVRInput.Get(OVRInput.Axis2D.PrimaryThumbstick).x;
        currentSkateboardAngle += steerAngle * Time.deltaTime * rotationSpeed;
        skateboard.rotation = Quaternion.identity;
        skateboard.Rotate(skateboard.right, slopeAngle, Space.World);

        skateboard.Rotate(skateboard.up, currentSkateboardAngle,Space.World);
```
 handle input from the right trigger button on a VR controller to simulate a sliding motion and calculate the slide velocity based on the magnitude of the offset vector divided by the time it took to move (Time.deltaTime). Slide velocity represents how fast the controller moved forward.

```
 if (rightTriggerValue > 0.95f)
        {
            if (!isIndexTriggerDown)
            {
                isIndexTriggerDown = true;
                startPos = (OVRInput.GetLocalControllerPosition(rightController));
            }

            offset = skateboard.forward.normalized * (OVRInput.GetLocalControllerPosition(rightController) - startPos).magnitude;
            Debug.DrawRay(startPos, offset, Color.red, 0.2f);

            // Use the slide velocity to adjust my game (skateboard movement)
            float slideVelocity = offset.magnitude / Time.deltaTime;
            Debug.Log("Slide Velocity" + slideVelocity);

            //UpdateSkateboardMovement(slideVelocity);
        }
        else
        {
            if (isIndexTriggerDown)
            {
                isIndexTriggerDown = false;
                offset = Vector3.zero;
            }
        }
```
manage the movement and friction of the object
```
//this.transform.position = this.transform.position + (offset) * translationGain;
        float currentVelocity = movementRb.velocity.magnitude;
        movementRb.velocity = skateboard.forward * currentVelocity * (1 - GetFriction() * Time.deltaTime); // inscrease friction, speed down
        movementRb.AddForce(offset * movementSpeed); // Don't go through the ground anymore, using physics

        if (OVRInput.Get(OVRInput.Button.Four))
        {
            if (parkourCounter.parkourStart)
            {
                this.transform.position = parkourCounter.currentRespawnPos;
            }
        }
```
use button one and button to start and finish t-shape task,
press button three and rotate our heads at the time to adjust the position of the t-shape
```
private void UpdateInteractionTask()
    {
        if (OVRInput.Get(OVRInput.Button.One))
        {
            if (!selectionTaskMeasure.isCountdown && selectionTaskMeasure.startAllowed)
            {
                // spawn new t-shape
                selectionTaskMeasure.isTaskStart = true;
                selectionTaskMeasure.StartOneTask();
            }
        }
        if (OVRInput.Get(OVRInput.Button.Two))
        {
            if(selectionTaskMeasure.doneAllowed) 
            {
                // confirm and remove current t-shape
                selectionTaskMeasure.isTaskStart = false;
                selectionTaskMeasure.EndOneTask();
            }
        }
        if (OVRInput.Get(OVRInput.Button.Three))
        {
            if (oldHmdRot.HasValue)
            {
                // rotate t-shape
                selectionTaskMeasure.ChangeTShapeRotation(hmd.transform.rotation * Quaternion.Inverse(oldHmdRot.Value));
            }
            oldHmdRot = hmd.transform.rotation;
        }
        else
        {
            oldHmdRot = null;
        }
        if (OVRInput.Get(OVRInput.Button.Four))
        {
            if (oldHmdPos.HasValue)
            {
                // move t-shape
                selectionTaskMeasure.ChangeTShapePosition(hmd.transform.position - oldHmdPos.Value);
            }
            oldHmdPos = hmd.transform.position;
        }
        else
        {
            oldHmdPos = null;
        }
    }
```
the skateboard aligns with the slope of the terrain below it by adjusting its position and rotation accordingly. 
```
 float SlopeAlighment()
    {
        RaycastHit hit;
        // The skateboard slides on only streetLayer, other objects will be ignored.
        if (Physics.Raycast(hmd.transform.position, Vector3.down, out hit, Mathf.Infinity, streetLayer))
        {
            //skateboard.up = hit.normal; // Aligns the skateboard with the street 

            // change height of skateboard
            Vector3 position = skateboard.position;
            position.y = hit.point.y + this.skateboardHeightOffset;
            skateboard.position = position;

            return Vector3.SignedAngle(Vector3.up, hit.normal, Vector3.right);
        }

        return 0;
    }
```