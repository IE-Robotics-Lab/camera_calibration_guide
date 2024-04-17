
Camera Calibration and Image Processing Using ROS

This guide provides instructions on how to calibrate a camera and process images using the ROS framework. It includes the use of the camera_calibration and image_proc packages.
Prerequisites

    ROS Installation: Ensure that ROS (Robot Operating System) is installed on your system. The instructions here are based on ROS 1. For more information, refer to the official ROS installation guide.

    Packages Installation: Install the image_proc and camera_calibration packages. You can install these packages using the following command:

    bash

    sudo apt-get install ros-<distro>-image-proc ros-<distro>-camera-calibration

    Replace <distro> with your specific ROS distribution name (e.g., noetic).

    Camera and ROS Setup: Connect your camera to the computer and ensure it is recognized by ROS. The camera should publish raw images to a ROS topic.

Printing the Checkerboard

Print a checkerboard pattern to use for calibration. The pattern can be printed on any standard printer. For calibration purposes, a checkerboard of 8x6 (8 corners horizontally and 6 corners vertically) with each square measuring 30mm is recommended.
Calibration Process

    Run the Camera Calibration Node:
    Execute the camera calibration tool by using the following command:

    bash

    rosrun camera_calibration cameracalibrator.py --size 8x6 --square 0.30 image:=/usb_cam/image_raw camera:=/usb_cam

        --size 8x6: Specifies the checkerboard dimension as 8x6 corners.
        --square 0.30: Each square in the checkerboard is 30mm in size.
        image:=/usb_cam/image_raw: The ROS topic where the raw images are published.
        camera:=/usb_cam: The namespace for the camera parameters.

    Perform Calibration:
        Follow the on-screen instructions to capture multiple views of the checkerboard from different angles and distances.
        The GUI will display the captured images and the current calibration results.
        Adjust the camera and checkerboard position until the software has enough data to compute the camera parameters accurately.

    Save and Commit Calibration Data:
        Once the calibration is satisfactory, click the Save button in the GUI to save the calibration data.
        Click Commit to update the /camera_info topic with the new calibration data.

Image Processing

After calibrating the camera, you can run the image_proc node to start image processing:

bash

ROS_NAMESPACE=usb_cam rosrun image_proc image_proc

This command sets the namespace to usb_cam and runs the image_proc node, which subscribes to raw images and publishes various processed images (e.g., rectified images).
Conclusion

By following these steps, you can successfully calibrate a camera and set up image processing in ROS. Make sure to verify the camera's calibration periodically and recalibrate if necessary, especially if the camera setup changes.


# Given you have the calibration done
You can use the yaml and a launch file to load the calibration parameters and update it to the camera_info topic.


