# mjpeg_streamer
mpjeg_streamer for rpi camera computer vision and octprint using the python3-picamera2 library

This is a small modification to the example mjpeg_streamer from the raspberry pi camera2 code: https://github.com/raspberrypi/picamera2/blob/main/examples/mjpeg_server_2.py

The modification is to also allow a single snapshot url which is useful for tasks such as creating timelapse videos.

I have also added a .service file which allows this to launch at startup.

This is aimed at being a simple helper script for the octoprint community.

To use:
1. Install the raspberry pi camera2 python libraries: sudo apt install python3-picamera2
2. Clone this repository.
3. Run via: python3 mjpeg_server_octoprint.py
4. Access the mjpg stream in your browser via: http://YOURIPADDRESS:8080/stream.mjpg or access a single snapshot via http://YOURIPADDRESS:8080/single

To run at startup: 
1. Edit the file webcamd.service and change the ExecStart=... line so that it points at the location you created the python file.
2. copy webcamd.service to /etc/systemd/system/
3. reload systemd: sudo systemctl daemon-reload
4. enable the service: sudo systemctl enable webcamd.service
5. start the service: sudo systemctl start webcamd.service.


Once this is setup, you can integrate your camera into octopi via the following.

The first step is to make sure the Classic Webcam plugin is installed. This is usually bundled with octopi, but to confirm:

Log into your octopi website and go to Settings->Plugin Manager
1. Search for "Classic Webcam"
2. Make sure it is installed.

Then configure the Classic Webcam plugin:
1. Go to Settings->Classic Webcam
2. Add the Stream URL: http://YOUR_IP_ADDRESS:8080/stream.mjpg
3. Add the Snapshot URL: http://127.0.0.1:8080/single
4. Save

Finally, make sure the Webcam & Timelapse settings are correct:
1. Go to Settings->Webcam & Timelapse
2. Enable Webcam support
3. Enable Timelapse support
4. Choose "Classic Webcam" for your snapshot webcam
5. Choose "Classic Webcam" for your fallback webcam.
