a) 
We have picked Mallet, set it up and tested it to create a spam classifier, and did tests to check the accuracy of the classifier. The classifier has >97% accuracy on the test data we tested on.
Attached the mallet, classifier and data. 

bin\mallet import-dir --input sample-data\spam\train\* --output spam.mallet
 
bin\mallet train-classifier --input spam.mallet --trainer MaxEnt --trainer NaiveBayes --training-portion 0.9 --num-trials 10

bin\mallet train-classifier --input spam.mallet --output-classifier spam.classifier
 
bin\mallet classify-dir --input sample-data\spam\test\spam --output spam_test --classifier spam.classifier
 
bin\mallet classify-dir --input sample-data\spam\test\notspam --output notspam_test --classifier spam.classifier
 

b)
For this part we have taken data (multiple files) encompassing multiple topics(space, windows, cryptography, etc…). We then ran the below 2 commands to get the results. The assessment is given in 3rd part.

bin\mallet import-dir --input sample-data\train-data --output topics.mallet --keep-sequence --remove-stopwords --extra-stopwords stoplists/extra_list.txt
 
bin\mallet train-topics  --input topics.mallet  --num-topics 10 --output-state topic-state.gz  --output-topic-keys topic_keys.txt --output-doc-topics topic_composition.txt
 
c)
There are 2 result files topic_keys and topic_compostion. The keys contain 10 lines, with each line having keys specific to that class\topic. For example one of the topics in our data was space related, so we got keys as space, nasa, earth, astronauts, etc… and for another class which was related to religion we got keys as god, jesus, etc… The composition contains the number of lines equal to the number of files, with each line having the number, file name and 10 values where each value is showing the strength corresponding to each topic. For example the document with names starting with sci.space are on topic space and you can see that the values at index 4(0 based index) is high, compared to other values and if you see the topic_keys for index 4(0 based index), the words/keys are relates to space. There is a similar pattern for all the files. We also included extra stop words to improve the accuracy.

As per our analysis, if we increase the number of topics to a large number, that there are classes. For example if we give number as 1000 when we have just 10 classes. The results might not be as satisfactory as we require it to be. 

Setting up the environment might be a difficult for a non-computer-savvy social scientist. Once he\she knows how to use the system and the commands to run it, it might not be that difficult. However, there are multiple classifiers which can be used in mallet. A non-computer-savvy social scientist might not understand what naïve Bayes is or what decision tree. This might limit his/her usage of the classifier.
