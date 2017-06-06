var cmd = 'gst-launch-1.0';
var args = ['autovideosrc', 'horizontal-speed=1', 'is-live=true',
    '!', 'videoconvert',
    '!', 'vp8enc', 'cpu-used=5', 'deadline=1', 'keyframe-max-dist=10',
    '!', 'queue', 'leaky=1',
    '!', 'm.', 'autoaudiosrc',
    '!', 'audioconvert',
    '!', 'vorbisenc',
    '!', 'queue', 'leaky=1',
    '!', 'm.', 'webmmux', 'name=m', 'streamable=true',
    '!', 'queue', 'leaky=1',
    '!', 'tcpserversink', 'host=127.0.0.1', 'port=9001', 'sync-method=2'];

var child = require('child_process');
var gstreamer = child.spawn(cmd, args, {stdio: 'inherit'});

gstreamer.on('exit', function (code) {
    if (code != null) {
        console.log('GStreamer error, exit code ' + code);
    }
    process.exit();
});

var express = require('express')
var app = express();
var http = require('http')
var httpServer = http.createServer(app);

httpServer.on('request', function(request, response) {

});
console.log(0);
app.get('/', function (req, res) {
    var date = new Date();
    console.log(1);
    res.writeHead(200, {
        'Date': date.toUTCString(),
        'Connection': 'close',
        'Cache-Control': 'private',
        'Content-Type': 'video/webm',
        'Server': 'CustomStreamer/0.0.1',
    });
    console.log(2);
    var net = require('net');
    var socket = net.connect(9001, function () {
        console.log(3);
        socket.on('close', function (had_error) {
            console.log(4); //skipped cause no error
            res.end();
        });
        socket.on('data', function (data) {
	        console.log(5); //stays here while streaming video
	    
            res.write(data);
        });
    });
    socket.on('error', function (error) {
        console.log(6);
        console.log(error);
    });
});

httpServer.listen(8001);
