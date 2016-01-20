setting image path
---------- 
* create 2 directory on my account: images and _tempmkdir <br />
			```
			mkdir images _temp
			```

* pull some images to directory 'images' 

* print path to file 'temp.txt'<br />
			```
			find `pwd`/images -type f -exec echo {} \; > _temp/temp.txt
			```

* because all file need labels, append 0 after each path<br />
		```
		sed "s/$/ 0/" _temp/temp.txt > _temp/file_list.txt
		```

setting architecture 
--------
* mean file 'imagenet_mean.binaryproto' has already been downloaded in /home/bmc/Desktop/caffe-master/data/ilsvrc12, thus we don't need to download it again.

* copy and modify the network definition(stored in /home/bmc/Desktop/caffe-master/examples/feature_extraction/imagenet_val.prototxt). We’ll be using the ImageDataLayer, which will load and resize images for us.
	```
	cp /home/bmc/Desktop/caffe-master/examples/feature_extraction/imagenet_val.prototxt _temp
	```
	in this file, we need to modify some parameters to make the input data work properly. Open imagenet_val.prototxt
	```
	vim _temp/imagenet_val.prototxt
	```
	change the source path to **_temp/file_list.txt** and mean_file path to **/home/bmc/Desktop/caffe-master/data/ilsvrc12/imagenet_mean.binaryproto**
	
extract features
--------
* everything has been set up, we can extract features use the command below. The number **1** means how many batches waiting to be extracted. The batch_size is defined in the file _imagenet_val.prototxt, you need to make sure **batch_number*batch_size >= number_of_images**
```
/home/bmc/Desktop/caffe-master/build/tools/extract_features.bin /home/bmc/Desktop/caffe-master/models/bvlc_reference_caffenet/bvlc_reference_caffenet.caffemodel _temp/imagenet_val.prototxt fc7 _temp/features 1 lmdb
```
* Cong! Now features have been extracted and stores in lmdb format in directory _temp/features

Conclusion
----------
* You have successfully extracted features, you need to convert lmdb format data into .mat format for matlab use.
* the architecture we used for extraction is [AlexNet](http://papers.nips.cc/paper/4824-imagenet-classification-with-deep-convolutional-neural-networks.pdf), we extracted in layer fc7.
