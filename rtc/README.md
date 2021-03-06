<h1> RTCPeer </h1>

<p>Note : this code is just used for local netowrk rtc peer conenctions, but if you add somtimeout until all ices generated it may work</p>
<p>Simple wrapper for RTCPeerConnection to make creation of RTC connection easy. </p>

<p>Suppose you have to peer machines where peer1 is running on first machine and peer2 is running on machine2, you can the following steps to create RTC Connection between these two peers :  </p>

<p>RTCPeer Creation (three steps) : </p>

<p>1- Connection initialization</p>

```javascript
var peer1 = new RTCPeer();
peer1.createConnection(null,{	//null is for ice servers so the code will work on LAN.
streams : [stream],	 //share streams.
channels : ['default'] //crate data channels.	
},callback); 
//after connection creation you should wait for couple
//of seconds so the ice candiates will be created, or you
//use optional callback function as thrid parameter.				
                                                                           

var connectionDescriptor1 = peer1.connectionDescriptor();// Now you should send this json object to the second machine, so the 
                                                         // second peer will use this connection

```

<p>2- Use the first peer connection descriptor</p>

```javascript
  var peer2 = new RTCPeer();  
  peer2.connect(connectionDescriptor1,callback);//Connects using descriptor, and creates its own connection descriptor.
				       //Wait for couple of seconds,or use optional callback function.
                                        
  var connectionDescriptor2 = peer2.connectionDescriptor();// Now you should send this json object to the first machine.
```

<p>3- Use the second peer connection descriptor</p>

```javascript
peer1.connect(connectionDescriptor2);
```

<p>All done!</p>

<p>Once the above steps done, you can access the shared stream and exchange channel messages.</p>

<p>Shared Steams : </p>

```javascript
  peer2.getPeerConnection().getRemoteStreams();
```
<p>Connection Channels : </p>

```javascript
  peer.connectionChannels();//Now you can use the created channels,you can use 'send' and 'onmessage' handler to exchange messages
                            //between the created peers
```
