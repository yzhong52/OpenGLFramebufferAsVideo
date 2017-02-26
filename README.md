Save OpenGL Framebuffer As Video
================================

We can save the OpenGL rendering result to a video using OpenCV buildt-in VideoWriter class. There are three steps:

**Create a video file to write**

 - Read OpenGL framebuffer
 - Close the video file
 - Create a Video File to Write

"video.avi" is the name of the file to save, 20.0f is fourcc, width and height are the size of the window. Finally, true indicate that we are saving

    cv::VideoWriter outputVideo;
    outputVideo.open( "video.avi", -1, 20.0f, cv::Size( width, height ), true);

**Read OpenGL framebuffer**

    cv::Mat pixels( height, width, CV_8UC3 );
    glReadPixels(0, 0, width, height, GL_RGB, GL_UNSIGNED_BYTE, pixels.data );
    cv::Mat cv_pixels( height, width, CV_8UC3 );
    for( int y=0; y<height; y++ ) for( int x=0; x<width; x++ ) 
    {
        cv_pixels.at<cv::Vec3b>(y,x)[2] = pixels.at<cv::Vec3b>(height-y-1,x)[0];
        cv_pixels.at<cv::Vec3b>(y,x)[1] = pixels.at<cv::Vec3b>(height-y-1,x)[1];
        cv_pixels.at<cv::Vec3b>(y,x)[0] = pixels.at<cv::Vec3b>(height-y-1,x)[2];
    }
    outputVideo << cv_pixels; 

**Close the video file**

    outputVideo.release();

Sample Code On [Github](https://github.com/yzhong52/Save-OpenGL-Framebuffer-As-Video). 

This sample code shows how to save OpenGL framebuffer to a video using OpenCV. The openGL code is borrowed from [HeHe Lesson 05](http://nehe.gamedev.net/tutorial/3d_shapes/10035/).

The necessary libs and dlls are included in the project; therefore, you don't need to install OpenCV on your machine if you don't want to.  
