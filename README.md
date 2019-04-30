# duckieGUI
A QT GUI interface to publish destination points for duckiebot to travel to

This is based off of the qt_tutorials package --- specifically the qtalker implementation

------------------------------------------------------------------------
# Implementation 
------------------------------------------------------------------------

### Note: Early Prototype of Development --- Not Finalized

### Instructions on how to run:

1. ```catkin build```

2. ```rosrun duckieGUI qtalker```

3. On the side of the GUI window, check "use environment variables"

4. Click "connect" --- if you click the buttons before hitting connect, the GUI will crash

5. The window should be resized so that P1 is in the very top left. This is due to a bug with the QT UI layout. 

6. The buttons can then be clicked and will advertise <geometry_msgs::Point> messages on "/trajectory/car1"

------------------------------------------------------------------------
# Changing Things
------------------------------------------------------------------------

### To change the background image
First, add your image under duckieGUI/resources/images. Second, edit the file images.qrc under duckieGUI/resources, 
and then add...
```
<RCC>
    <qresource prefix="/" >
        <file>images/icon.png</file>
		    <file>images/duckietown_example.png</file>
        <!-- ADD YOUR IMG HERE -->
        <file>images/your_image_here.png</file>
    </qresource>
</RCC>
```

### To Add/Change Points
In the file under duckieGUI/common/main_window.cpp and main_window.hpp

If you would like to add a button corresponding to point18 - with the duckietown coordinates of (x = 2.3, y = 1.8),
create a QT PushButton titled "point18" and add it to the grid interface in duckieGUI/ui/main_window.ui. Then in the file
main_window.cpp, add the following function:

```
void MainWindow::on_point18_clicked(bool check) {
    qnode->advertisePoint(2.3,1.8);
}
```

In main_window.hpp of course, also add the function declaration under public Q_SLOTS:
```
void on_point18_clicked(bool check);
```

------------------------------------------------------------------------
# Problems that need to be solved
------------------------------------------------------------------------
1. Crashing that happens if you hit the points before it connects
2. Resizing issue with the QT grid system
3. Only can specify the destination points
4. Has not been tested in conjunction with duckie_shells pacakge that would use it
5. Has not been tested in implementation


------------------------------------------------------------------------
