# webcam
Accessing your webcam via your browser used to involve a...pardon the profanity, a plugin. That's right. In order to connect to a webcam and gain access to its video stream, you had to rely on something primarily created in Flash or Silverlight. While that approach certainly worked for browsers that supported plug-ins, it didn't help for the increasing number of browsers that aim to be plugin-free. This inability to natively access the webcam without relying on 3rd party components was certainly a gap in the HTML development story. At least, that was the case until pretty recently.

How to Use Webcam In PHP:
Here we will use the JPEG Camera script for the webcam functions to take the snap and save it.
index.php
<script type="text/javascript" src="https://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js"></script>
<script src="jpeg_camera/jpeg_camera_with_dependencies.min.js" type="text/javascript"></script>
Below the form we will put our webcam window to show the webcam screen capture.
     <div class="col-md-6">
         <div class="text-center">
     <div id="camera_info"></div>
    <div id="camera"></div><br>
    <button id="take_snapshots" class="btn btn-success btn-sm">Take Snapshots</button>
    </div>
    </div>
    Now it's time to process the image snap. Add this code to index.php :
    
  <script>
  var options = {
      shutter_ogg_url: "jpeg_camera/shutter.ogg",
      shutter_mp3_url: "jpeg_camera/shutter.mp3",
      swf_url: "jpeg_camera/jpeg_camera.swf",
    };
    var camera = new JpegCamera("#camera", options);
  
  $('#take_snapshots').click(function(){
    var snapshot = camera.capture();
    snapshot.show();
    console.log(snapshot);
    snapshot.upload({api_url: "action.php"}).done(function(response) {
$('#imagelist').prepend("<tr><td><img src='"+response+"' width='100px' height='100px'></td><td>"+response+"</td></tr>");
}).fail(function(response) {
  alert("Upload failed with status " + response);
});
})

function done(){
    $('#snapshots').html("uploaded");
}
</script>

Now when we receive the success message, we will show it in a table.
  <table class="table table-bordered">
      <thead>
          <tr>
            <th>Image</th><th>Image Name</th>
          </tr>
      </thead>
      <tbody id="imagelist">    
      </tbody>
   </table>
        
 You can also use getUserMedia in index2.php and index3.php
