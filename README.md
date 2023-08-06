Imagine having IP cameras that stream video feed over RTSP or having video captured from your laptop's webcam, and you wish to visualize this content in real-time with extremely low latency, securely over TLS, within your web browser or on a grafana dashboard because maybe you want to build an home monitoring dashboard.
You can achieve this by configuring go2rtc, a server that provides the shortest streaming latency possible and is effortless to set up on any operating system. You can checkout this fantastic project on its official GitHub repository: https://github.com/AlexxIT/go2rtc.

In this repository, I demonstrate how you can in 1 minute, see your live camera feed on a grafana dashboard (or just in the browser). Here are the steps:

1. Modify the `go2rtc-config/go2rtc.yaml` file with your desired source. I already left two examples in the file, but you can find additional examples and configuration settings at this link: https://github.com/AlexxIT/go2rtc#module-api.

2. Customize the Grafana dashboard to display the live camera stream using a 'Text' panel and embedding the WebRTC stream inside an Iframe. To do so you can update the content tag within `grafana/dashboard/dashboards/dashboard.json` with your specific Iframe. For example, if your go2rtc server is running on localhost and the web UI is on port 1984, and the stream name you configured in `go2rtc-config/go2rtc.yaml` is 'dahua', the live camera will be shown in the browser at http://localhost:1984/stream.html?src=dahua&mode=webrtc, so you can use the following Iframe:

   ```html
   <iframe width="1000" height="1000"
   src="http://localhost:1984/stream.html?src=dahua&mode=webrtc">
   </iframe>
4. Launch go2rtc and Grafana in separate containers using ```docker-compose up -d```.
5. Access the Grafana dashboard at http://localhost:3000 and the go2rtc web UI at http://localhost:1984.


