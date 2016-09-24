cvui
=====
A (very) simple UI lib built on top of OpenCV drawing primitives. Other UI libs, such as [imgui](https://github.com/ocornut/imgui), require a graphical backend (e.g. OpenGL) to work, so if you want to use imgui in a OpenCV app, you must make it OpenGL enabled, for instance. It is not the case with cvui, which uses *only* OpenCV drawing primitives to do all the rendering (no OpenGL or Qt required).

![image](https://raw.githubusercontent.com/Dovyski/depository/master/cvui.png?20160819)

Features
--------
- Lightweight and simple to use user interface.
- No external dependencies (except OpenCV).
- Based on OpenCV drawing primitives only (OpenGL or Qt are not required).
- Friendly and C-like API (no classes/objects, etc).
- Easily render components without worrying about their position (using rows/columns).
- MIT licensed.

Build
-----
The only dependency is OpenCV (version 2.xx and 3.0), which you are probably already using. Just add `cvui.h` and `cvui.cpp` to your project and you are ready to go.

Usage
-----
Check the [examples](https://github.com/Dovyski/cvui/tree/master/example) folder for some code, but the general idea is the following:

```c++
#include <iostream>
#include <opencv2/core/core.hpp>
#include <opencv2/highgui/highgui.hpp>
#include "cvui.h"

int main(int argc, const char *argv[])
{
	cv::Mat frame = cv::Mat(250, 600, CV_8UC3);
	bool checked = false;
	int count = 0;

	cvui::init("CVUI Test");

	// optional user defined mouse callback (can be a lambda or std::function)
	cvui::MouseCallback mouseCallback = [&](int event, int x, int y, int flags, void * data) -> bool{
		std::cout << "Mouse callback at	" << x << ", " << y << std::endl;
		return false;
	};
	cvui::setMouseCallback(&mouseCallback);

	while (true) {
		frame = cv::Scalar(49, 52, 49);

		cvui::text(frame, 50, 30, "Hey there!");
		cvui::text(frame, 200, 30, "Use hex 0xRRGGBB colors easily", 0.4, 0xff0000);

		if (cvui::button(frame, 50, 50, "Button")) {
			std::cout << "Button clicked!" << std::endl;
		}

		cvui::window(frame, 50, 100, 120, 100, "Window");
		cvui::counter(frame, 200, 100, &count);
		cvui::checkbox(frame, 200, 150, "Checkbox", &checked);

		if (cvui::button(frame, 500, 50, "&Quit")) {
			break;
		}

		cvui::imshow(frame);
	}
	return 0;
}

```

License
-----
Copyright (c) 2016 Fernando Bevilacqua. Licensed under the MIT license.

Change log
-----
See all changes in the [CHANGELOG](https://github.com/Dovyski/cvui/tree/master/CHANGELOG.md) file.
