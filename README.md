# Wave the rover Gazebo sim

Custom URDF model and meshes are joined together with a custom bracket.
![image](https://github.com/user-attachments/assets/3887ecf5-f077-4465-9561-501923fa0463)



Custom cone models for Gazebo.
![image](https://github.com/user-attachments/assets/640433f0-93a7-4d19-92df-2fe1d83b8f02)

Custom tracks.
![image](https://github.com/user-attachments/assets/383d5c66-a3c4-49bc-ad41-f0b44ab5fc89)

In the Gazebo sim.
![image](https://github.com/user-attachments/assets/c1a38ed7-a634-4eed-9590-a49b017c90d2)
![image](https://github.com/user-attachments/assets/51a6e535-0df8-4e2d-8738-be085da67fe3)


## Learnings
### URDF to SDF pose transformations
**URDF: Joint origins define the pose of the child link relative to the parent link.**

**SDF: Each link's <pose> is defined relative to its parent link, and joint poses are typically relative to the child link.**

Given this, when converting from URDF to SDF, you need to compute the absolute pose of each link by cumulatively applying the transformations defined by the joints in the URDF. This ensures that each link in the SDF has the correct position and orientation relative to the base link.

Here's how you can compute the poses:

    Start with the base link: Assume its pose is at the origin: (0, 0, 0, 0, 0, 0).

    Apply joint transformations: For each subsequent link, apply the joint's translation and rotation to the parent's pose to get the child's pose.

For example, if a joint has:

    Translation: (x, y, z)
    Gazebo Simulation

    Rotation: (roll, pitch, yaw)

Then the child link's pose is:

    Position: Parent's position plus the rotated translation vector.

    Orientation: Parent's orientation combined with the joint's rotation.


### Gazebo no camera found bug
Need to source the Gazebo setup file if this error is gotten on build of the world file 
```gazebo::rendering::Camera*]: Assertion `px != 0' failed.```

This is the fix
```. /usr/share/gazebo/setup.sh```
