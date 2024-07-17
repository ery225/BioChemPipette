# Automated BioChem Pipette Machine with Opentron-1

## Introduction
The Automated BioChem Pipette Machine with Opentron-1 is designed for biochemistry lab students to learn and automate the tedious process of precise liquid handling. This project aims to eliminate human error and improve the efficiency and accuracy of liquid handling tasks in a lab setting.

## Prerequisites
Softwares, hardwares, and anything else you need for this project.

**Software**
- Python 3.7 or under
- Python Virual Enviornment
- Opentron API (Version 2.5.2)
- CV2 API
- Matlab
- Numpy
- Linux PC or your personal laptop

**Hardware**
- USB to Machine Cable
![USB to Machine](OT-1/IMG_9910.jpg)

- Round Barrel Jack
![Round Barrel Jack](OT-1/IMG_9911.jpg)

- USB to USC Cable
![USB to USC Cable]()

- OT-1 Machine
![OT-1 Machine]()

- Intel RealSense Camera
![Intel RealSense Camera]()

- Camera Mount
![Camera Mount]()

- Containers
![Containers]()


## Installation
Steps to install the necessary software, tools, or libraries.
This is only necessary on personal laptop. Everything should have been setup on Linux PC.

1. **Install Python**:
    - Follow these steps to install Python. Make sure the version is 3.7 and under.
    - [Python Steps](https://phoenixnap.com/kb/how-to-install-python-3-windows)
    - [Python Installation](https://www.python.org/downloads/)

2. **Setup Python Virual Envrionment**:
    - Steps to create and activate virtual envrionment for Python.
    - [Venv](https://packaging.python.org/en/latest/guides/installing-using-pip-and-virtual-environments/)

## Setup Software
Steps to set up the project environment. All installations are done under the main folder that houses both the API and OT-1 folder. It does not necessarily matter but just in case.

1. **Clone the repository**:
    ```bash
    git clone https://github.com/yourusername/projectname.git
    cd projectname
    ```
2. **Install the API and Dependencies**:
    
    There is a chance where you need to install all these APIs and dependencies everytime you shut down the program.

    [Opentron Python](https://pypi.org/project/opentrons/)
    ```bash
    pip install opentrons==2.5.2
    ```

    CV2
    ```bash
    pip install opencv-python opencv-python-headless
    ```

    MatLab
    ```bash
    pip install matplotlib
    ```

    Numpy
    ```bash
    pip install numpy
    ```

    PyRealSense2
    ```bash
    pip install pyrealsense2
    ```

## Setup Hardware
Steps to set up the physical machine.

1. **Insert Round Barrel into Machine and Outlet Socket**

2. **Insert USB to Machine Cable**
- You should see the Smoothieboard glowing green and orange. Similar to photo on the bottom
![machine pre](OT-1/machine_pre.jpg)

3. **Click the power button**
- It should now glow a stable blue colour. The Smoothieboard should now take a red colour as well.
![machine post](OT-1/machine_post.jpg)

4. **If any problems arise, check Troubleshooting**



## Usage
Instructions on how to use the project.

We are going to run a couple of test/demo programs to make sure you are completely connected to the physical machine.

1. Make sure all the dependencies and APIs are there.

2. Open the OT-1 folder.

3. Make sure to change `robotUSB` to whatever port you are using.
  
4. Run `python test.py` to see if the OT-1 machine is connected and that it will move to raw coordinates.

5. Run `python test2.py` to see if the OT-1 machine is connected and that it will move to certain containers and initate the pipette process.

6. If you run into any issues, consult troubleshooting.

## Troubleshooting
Common issues and solutions.

**Pkg_Resources Issue**: The error ModuleNotFoundError: No module named 'pkg_resources' indicates that the pkg_resources module, which is part of the setuptools package, is not installed in your virtual environment.
```bash
Traceback (most recent call last):
  File "C:\Users\ericy\OneDrive\Desktop\BioChem\OT-1\test2.py", line 1, in <module>
    from opentrons import robot, instruments, containers
  File "C:\Users\ericy\OneDrive\Desktop\BioChem\.venv\Lib\site-packages\opentrons\__init__.py", line 4, in <module>
    from opentrons.robot.robot import Robot
  File "C:\Users\ericy\OneDrive\Desktop\BioChem\.venv\Lib\site-packages\opentrons\robot\__init__.py", line 1, in <module>
    from opentrons.robot.robot import Robot
  File "C:\Users\ericy\OneDrive\Desktop\BioChem\.venv\Lib\site-packages\opentrons\robot\robot.py", line 5, in <module>
    from opentrons import containers, drivers
  File "C:\Users\ericy\OneDrive\Desktop\BioChem\.venv\Lib\site-packages\opentrons\containers\__init__.py", line 5, in <module>
    from opentrons.containers.persisted_containers import get_persisted_container
  File "C:\Users\ericy\OneDrive\Desktop\BioChem\.venv\Lib\site-packages\opentrons\containers\persisted_containers.py", line 6, in <module>
    import pkg_resources
ModuleNotFoundError: No module named 'pkg_resources'
```
  - **Solution**: `pip install setuptools`

**Getargspec Error**: The error AttributeError: module 'inspect' has no attribute 'getargspec'. Did you mean: 'getargs'? indicates that the getargspec method is not available in the version of Python you are using. This method has been deprecated since Python 3.5 and removed in Python 3.9.

```bash
Traceback (most recent call last):
  File "C:\Users\ericy\OneDrive\Desktop\BioChem\OT-1\test2.py", line 38, in <module>
    transfer_droplet()
  File "C:\Users\ericy\OneDrive\Desktop\BioChem\OT-1\test2.py", line 24, in transfer_droplet
    pipette.pick_up_tip(tip_rack.wells('A1'))
  File "C:\Users\ericy\OneDrive\Desktop\BioChem\.venv\Lib\site-packages\opentrons\instruments\pipette.py", line 791, in pick_up_tip
    self.move_to(location, strategy='arc')
  File "C:\Users\ericy\OneDrive\Desktop\BioChem\.venv\Lib\site-packages\opentrons\instruments\pipette.py", line 257, in move_to
    self.robot.move_to(location, instrument=self, strategy=strategy)
  File "C:\Users\ericy\OneDrive\Desktop\BioChem\.venv\Lib\site-packages\opentrons\util\trace.py", line 15, in decorated
    if inspect.getargspec(f).defaults:
       ^^^^^^^^^^^^^^^^^^
AttributeError: module 'inspect' has no attribute 'getargspec'. Did you mean: 'getargs'?
```
  - **Solution**: The virtual enviornment is not utilizing Python 3.7 or under. Restart your virtual environment and make sure you select the correct interpreter.



**Limit Switch Hit**: The RuntimeWarning: Robot Error: limit switch hit indicates that the robot has encountered a hardware limit switch, which is a safety feature to prevent the robot from moving beyond its physical boundaries. This can happen if the robot is instructed to move to a location that is outside its allowable range.
```bash
Traceback (most recent call last):
  File "C:\Users\ericy\OneDrive\Desktop\BioChem\OT-1\test2.py", line 39, in <module>
    transfer_droplet()
  File "C:\Users\ericy\OneDrive\Desktop\BioChem\OT-1\test2.py", line 24, in transfer_droplet
    pipette.pick_up_tip(tip_rack.wells('A1'))
  File "C:\Users\ericy\OneDrive\Desktop\BioChem\.venv\Lib\site-packages\opentrons\instruments\pipette.py", line 791, in pick_up_tip
    self.move_to(location, strategy='arc')
  File "C:\Users\ericy\OneDrive\Desktop\BioChem\.venv\Lib\site-packages\opentrons\instruments\pipette.py", line 257, in move_to
    self.robot.move_to(location, instrument=self, strategy=strategy)
  File "C:\Users\ericy\OneDrive\Desktop\BioChem\.venv\Lib\site-packages\opentrons\util\trace.py", line 9, in decorated
    res = f(*args, **kwargs)
          ^^^^^^^^^^^^^^^^^^
  File "C:\Users\ericy\OneDrive\Desktop\BioChem\.venv\Lib\site-packages\opentrons\robot\robot.py", line 476, in move_to
    self._driver.move_head(**coord)
  File "C:\Users\ericy\OneDrive\Desktop\BioChem\.venv\Lib\site-packages\opentrons\drivers\smoothie_drivers\v2_0_0\driver.py", line 381, in move_head
    self.move(mode, **kwargs)
  File "C:\Users\ericy\OneDrive\Desktop\BioChem\.venv\Lib\site-packages\opentrons\drivers\smoothie_drivers\v2_0_0\driver.py", line 344, in move
    raise e
  File "C:\Users\ericy\OneDrive\Desktop\BioChem\.venv\Lib\site-packages\opentrons\drivers\smoothie_drivers\v2_0_0\driver.py", line 339, in move
    self.send_command(self.MOVE, **args, m400=True, timeout=300)
  File "C:\Users\ericy\OneDrive\Desktop\BioChem\.venv\Lib\site-packages\opentrons\drivers\smoothie_drivers\v2_0_0\driver.py", line 279, in send_command        
    return self.readline_from_serial(timeout=timeout)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File "C:\Users\ericy\OneDrive\Desktop\BioChem\.venv\Lib\site-packages\opentrons\drivers\smoothie_drivers\v2_0_0\driver.py", line 180, in readline_from_serial
    self.detect_smoothie_error(str(msg))
  File "C:\Users\ericy\OneDrive\Desktop\BioChem\.venv\Lib\site-packages\opentrons\drivers\smoothie_drivers\v2_0_0\driver.py", line 293, in detect_smoothie_error
    raise RuntimeWarning(error_msg)
RuntimeWarning: Robot Error: limit switch hit
```
**Solution**: Sometimes it happens. Run the script a couple of times.

**Unstable Round Barrel Jack Power and Machine Power**: If the machine's power button starts flashing a blue color, or no colour at all, there is one of three possible scenarios:
- Smoothieboard is overloaded
- Power cable is tripping
- Machine is not connected efficiently.

Check the last option first. Make sure all the ports are correct and all the wires and cables are connected correctly as well. Keep running tests if possible. If it is the other two scenarios, it woud take ages to repair. Be patient and ask a for guidance if needed.

## Other Resources
These are some resources I found particularly help. Please utilize them.

[Types of Labware](https://docs.opentrons.com/ot1/containers.html#:~:text=groups%20of%20wells.-,Labware%20Library,Note)
[Connecting Intel RealSense Camera with Python](https://www.youtube.com/watch?v=CmDO-w56qso)


## Contact
For any inquiries or further information, please contact me at:

- **Email**: ericyang005@gmail.com
- **Phone Number**: (508)-468-1718