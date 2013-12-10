Vitruvius
=========

Vitruvius is a set of easy-to-use Kinect utilities that will speed-up the development of your projects.

Features
---

*Skeletal extensions*
* Joint scaling, proper for on-screen display
* User height
* Distance between joints

*WPF extensions*
* Easily display color and depth frames in WPF
* Save Kinect frames as bitmap images

*Coming soon*
* Kinect for Windows v2 support
* Gesture support
* Posture support

Installation
---
You can install Vitruvius using one of the following methods:

1. Easiest way: Create a new WPF project in Visual Studio and select

        Tools ➙ Library Package Manager ➙ Manage NuGet Packages for Solution

then search for Vitruvius and click Install.

2. Install via NuGet command-line

        PM> Install-Package Vitruvius

3. Download project and build the solution

Examples
---

1. Displaying Kinect color frames:

        void Sensor_ColorFrameReady(object sender, ColorImageFrameReadyEventArgs e)
        {
            using (var frame = e.OpenColorImageFrame())
            {
                if (frame != null)
                {
                    // Display on screen
                    image.Source = frame.ToBitmap();
                    
                    // Capture JPEG file
                    frame.Capture("C:\\ColorFrame.jpg");
                }
            }
        }
        
2. Displaying Kinect depth frames:

        void Sensor_DepthFrameReady(object sender, DepthImageFrameReadyEventArgs e)
        {
            using (var frame = e.OpenDepthImageFrame())
            {
                if (frame != null)
                {
                    // Display on screen
                    image.Source = frame.ToBitmap();
                    
                    // Capture JPEG file
                    frame.Capture("C:\\DepthFrame.jpg");
                }
            }
        }
        
3. Drawing a skeleton and getting its height:

        void Sensor_SkeletonFrameReady(object sender, SkeletonFrameReadyEventArgs e)
        {
            using (var frame = e.OpenSkeletonFrame())
            {
                if (frame != null)
                {
                    canvas.Children.Clear();
                    
                    var skeletons = frame.Skeletons();
                    
                    foreach (var skeleton in skeletons)
                    {
                        if (skeleton != null)
                        {
                            if (skeleton.TrackingState == SkeletonTrackingState.Tracked)
                            {
                                // Draw the skeleton.
                                canvas.DrawSkeleton(skeleton, Colors.LightCyan);
                                
                                // Get the skeleton height.
                                double height = skeleton.Height();
                            }
                        }
                    }
                }
            }
        }

Prerequisites
---
* [Kinect for Windows](http://amzn.to/1k7rquZ) or [Kinect for XBOX](http://amzn.to/1dO0R0s) sensor
* [Kinect for Windows SDK v1.8](http://go.microsoft.com/fwlink/?LinkID=323588)

License
---
You are free to use these libraries in personal and commercial projects by attributing the original creator of Vitruvius. Licensed under [Apache v2 License](https://github.com/LightBuzz/Vitruvius/blob/master/LICENSE).
