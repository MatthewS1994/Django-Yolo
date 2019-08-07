# Django Recognize files uploaded by Yolo


## How it works
First you need to add yolo.weights file to bin folder <br>
<pre><code>
python manage.py runserver
</code></pre>
## I've recorded the progress as I'm working on it.
1. defaults.py Change the default setting in to make it immediately executable without args

2. return Code disassembly to get the value
 Find out where the code to run the classification and return the image
tfnet.predict () in cliHandler (args) in the cli.py file in the flow file-> darkflow folder (after __init__ is executed first) + TFNet.predict-> net Predict () in flow.py file in folder-> feed_dict in predict-> mess in boxresults of predict.py in yolo folder (imgcv, mess in postprocess)
 Conclusion: replace clinet's tfnet.predict () with tfnet.return_predict (image) but not returning yet
Make file paths easier (I want to get the path of defaults)
Only those things that have some confidence are to be extracted and True if any of the return values ​​are a person.



3. django of views.py The process of planting yolo on
 Moved yolo files to the location where manage.py resides
 If you run python manage.py -runserver, runserver will run over to sys.argv and you will get an error when you run yolo.
-> subtract sys.argv from cliHandler (sys.agrsv) in views.py
   I removed args from cliHandler (args) in cli.py and deleted FLAG.parseArgs (args)

4. Detail process
 The final return of viewsd returns the yolo result with HttpResponse (cliHandler (image_name))
 The analysis file is the file name (request.FILES ['photo']) passed from the photos folder path + views.
 Pass it to json: first make a shell in dict format (result = {}) and use .update to put it in dict format and then change it to json.dumps ()





## yolo source 
https://pjreddie.com/darknet/yolo/
