Some explinations about the rosbag files:
=========================================

When doing experiment, I recorded everything using rosbag including gmapping's results. But later I found in the data there was noise caused by my computer's lid. To remove the noise, I need to remove gmapping's results from the rosbags. 

The initial rosbags are put into the folder "InitialBags(Noise)". Probably you wouldn't use them. Just keep them in case.

The cleanned rosbags are the ones starting with "modi_" in their names. They were cleaned using "removeGmappingRosbagInfo.ipynb", to removed the gmapping related topics. So these files only include:
		1. LRF scan
		2. Robot odometry 



About performance of my method on these rosbags:
================================================

My method cannot work well in "modi_B2F1", "modi_B3F1" and "modi_B3F2". (So I didn't mention them in my thesis.) Mainly because the glass in these environments is too clean and thus its occupancy probability is too low. Therefore, even the filtering threshold for glass was reduced, the glass was still filtered out as noise. I talked about this problem in the file "Problems and Possible Solutions.txt".
