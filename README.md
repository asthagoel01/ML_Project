# Automating_Change_in_Hyperparameters_for_increasing_Model_Accuracy

What is the Purpose of this Project?

We make Model in ML so we can find a formula using experiences.
Here,we also made some Model but The Accuracy of the Model really matters a lot because in today's world ,almost everything is dependent on Machine auto Intelligence(comes from the Model) and so the correctness of the Model matters alot.

But it becomes hectic to make a good model because of many hyperparamaters(parameters which we need to set by own) so as to acheive good Accuracy and takes Much Time.

But in today's world,we have became much dependent on machines that we can't wait much ,also can't do such manual things in machinees world.

So,here I tried to automate the process of changing hyperparameters.Although there are many hyperparameters we need to change to acheive Wished accuracy.

Here I tried to automate the updating of hyperparameter(No. of neurons) such that it not remain insufficient or attain Overfitting with the help of ML and DevOps.
Because,
Less Neurons becomes insufficient for traning and making general formula ,in short, good model can't be acheived.
More Neurons do Overfiiting,means learn dataset or a same pattern so Model not expertise on different-different patterns.

...................................................Tools and Technologies used................................................................................

Docker(to run model files)
Python(Programming Language)
ML(Technology for making and optimising model)
Jenkins(to integrate and automate the whole process of updation and notification)

-------------------------------------------------------------Here are steps for my task--------------------------------------------------------------------

1. Created container image that’s has Python3 and Keras or numpy installed using dockerfile (When we launch this image, it should automatically starts train the model in the container).

2. Created a job chain of T3Job1, t3j2, t3j3, t3j4 and t3j5 using build pipeline plugin in Jenkins.

T3Job1 : Pull the Github repo automatically when some developers push repo to Github.
t3j2 : By looking at the code or program file, Jenkins should automatically start the respective machine learning software installed interpreter install image container to deploy code and start training( eg. If code uses CNN, then Jenkins should start the container that has already installed all the softwares required for the cnn processing).
t3j3 : Train your model and predict accuracy or metrics.
t3j4 : if metrics accuracy is less than 80% , then tweak the machine learning model architecture and Retrain the model.

3. Notify Developer that the best model is created to developer by sending email.

4. Created One extra job t3j6 for monitor : If container where app is running. fails due to any reason then this job should automatically start the container again from where the last trained model left.

![image](https://user-images.githubusercontent.com/62610706/137878985-5a3266ef-f3c1-4a6e-b6b2-34275e1687af.png)


..............................................................................Lets Start.........................................................................................

1. Create container image that’s has Python3 and Keras or numpy installed using the Dockerfile.

![image](https://user-images.githubusercontent.com/62610706/137864714-e86b98e3-36da-4fb8-82d6-5692b6c844a8.png)


                                    Dockerfile for image t3:v1.\

2.

T3Job1: Pull the Github repo automatically when some developers push repo to Github.

Code written for developing ML Model is written by Developer in FinalModel.py(I am, in this case) and this code is pushed by Developer into Github Repo(https://github.com/asthagoel01/mlt3.git) using Git Bash(in this case).

![image](https://user-images.githubusercontent.com/62610706/137864774-5f3ad5de-5fc3-412e-b5ed-d8390c93e2be.png)
![image](https://user-images.githubusercontent.com/62610706/137864874-a6244082-9ee0-46a8-8e5e-ca0b0db34cdd.png)

Now,code present on Remote repository https://github.com/asthagoel01/mlt3.git will be triggered using Poll SCM trigger so that,updates will be there in Every seconds.
![image](https://user-images.githubusercontent.com/62610706/137864944-94e12852-8ae4-4f49-b864-cff12e597dab.png)
![image](https://user-images.githubusercontent.com/62610706/137864985-0729a48c-86c3-4c6a-b169-7cccbd0d05fa.png)
Output for the program;
![image](https://user-images.githubusercontent.com/62610706/137865050-2d7d497b-bb93-4039-b937-bf9c090bcb34.png)


t3j2 : By looking at the code or program file, Jenkins should automatically start the respective machine learning software installed interpreter install image container to deploy code and start training( eg. If code uses CNN, then Jenkins should start the container that has already installed all the softwares required for the cnn processing).

I run check.py file(file to check which type of ML Model it is) where we read the file in which code for model is written(FinalModel.py, in this case) and if word convD is found anywhere then CNN will be printed which indicates that this model is a CNN model.

So,now the Model(developed and pushed by Developer) will run in a docker container using image t3:v1(this image contains all the libraries which are required for CNN model).

![image](https://user-images.githubusercontent.com/62610706/137865154-76510f6e-0777-4d40-ae7c-a344d5f7ff86.png)

![image](https://user-images.githubusercontent.com/62610706/137865185-726b0fb6-31c7-40d3-989f-5b1cdc77c109.png)


Note: The Reference for check.py is:https://github.com/asthagoel01/trying.git.

![image](https://user-images.githubusercontent.com/62610706/137865261-97324938-334f-4bbb-ac82-5598c0d1a8a9.png)
![image](https://user-images.githubusercontent.com/62610706/137865314-a4dce45c-7bb9-4426-bc8f-938f9ee6c9a0.png)
![image](https://user-images.githubusercontent.com/62610706/137865337-e99091b3-f611-4ef4-9aa1-bbb3549ed2e1.png)
![image](https://user-images.githubusercontent.com/62610706/137865362-13b759ed-5ac7-41d7-a488-248c8d4674b1.png)

t3j3 : Train your model and predict accuracy or metrics.

Now,the docker container in which Model(in FinalModel.py) was trained in t3j2 will be restarted and accuracy of the Model can be seen.

![image](https://user-images.githubusercontent.com/62610706/137865442-2adf71fe-f128-4026-bf68-c53e62fc9914.png)
![image](https://user-images.githubusercontent.com/62610706/137865482-f0e1505a-b704-496e-a9af-40c38f7f9311.png)
![image](https://user-images.githubusercontent.com/62610706/137865504-44163166-f8d2-4abc-9049-344b3c707557.png)

t3j4 : if metrics accuracy is less than 80% , then tweak the machine learning model architecture and Retrain the model.

I made a new folder pre.
In this folder,I copied model(FinalModel.py) pushed by developer(present in T3Job1 workspace) and a text file that contains accuracy of the model(accuracy.txt).
So,I restarted docker container in which FinalModel.py was run in t3j2 so that,the text file(generated by Python Code) stored in Docker Container can be accessed and accuracy of the Model can be shown.

If the Accuracy of model is not 0.99 or 99%(which we assumes the Best Accuracy)then we will run tweak.py file (Contains code to tweak the Model by tweaking the hyperparameter(No. of Neurons) so that Accuracy of Model can increase) in a new docker container using image that has interpreter(to run tweak.py) installed already,so that 99% Acurracy can be acheived.

![image](https://user-images.githubusercontent.com/62610706/137865603-cadb9d55-b34c-4ca8-9aef-b253a8ba81bc.png)

![image](https://user-images.githubusercontent.com/62610706/137865630-5c697118-4688-4eed-bfe7-5a228763a2cb.png)

Reference for this file(tweak.py):https://github.com/asthagoel01/trying.git.

Note: tweak.py file will be developed by Developer as It is developer only who knows how to improve accuracy in the Real World. I am just trying to show how to automate the process. 

![image](https://user-images.githubusercontent.com/62610706/137865723-3b949e20-d730-4b4c-8ed3-f5064928e207.png)

Now, After comparing Accuracy,the Accuracy was found 0.9746 so,now tweak.py file will run to improve the accuracy of Model by increasing No. of Neurons in every turn until 99% Accuracy acheived.

I wanted to acheive 99% Accuracy but if accuracy is decreasing instead of increasing(sometimes ,more no. of neurons do overfitting(because more neurons,learn pattern of dataset and fails for the new images) which we definitely not want) so in that case I conclude with Best Accuracy till that time inspie of re-training model again and again and for this, inside the tweak.py file ,after tweaking and retraining the model,I also compare last accuracy with current and If current Accuracy is less than Previous Accuracy so,further model will not retrain and loop will be exited so that Best Accuracy(Previous Accuracy) will be shown.

![image](https://user-images.githubusercontent.com/62610706/137865803-ec2b0882-09c4-43f9-ae24-76c537f0af74.png)

![image](https://user-images.githubusercontent.com/62610706/137865830-7a3bad27-f616-4505-a89d-3cafc6aaad73.png)

![image](https://user-images.githubusercontent.com/62610706/137865854-9b91d860-45dd-45db-ba5e-787e3a0be0b0.png)
![image](https://user-images.githubusercontent.com/62610706/137865913-10109004-6132-4211-b2c9-1cb6bc4d1cea.png)
![image](https://user-images.githubusercontent.com/62610706/137865941-d729efeb-f5cb-4546-93a2-334a93fbdc42.png)

![image](https://user-images.githubusercontent.com/62610706/137866000-8194a8cb-9d71-4209-afaf-2dded1169af8.png)
![image](https://user-images.githubusercontent.com/62610706/137866042-8f594c6a-0c03-4f05-8e21-bf90a9914d84.png)

3.
Notify Developer that the best model is created to developer by sending email.

On Best Accuracy Acheived ,mail will be sent to the Developer.

![image](https://user-images.githubusercontent.com/62610706/137866129-678de41a-32f0-4d5c-b92d-6b5f3f469b31.png)

Note: For Successfully sending email,I used email-extension plugin.After installing the plugin,we need to do these things also in Manage Plugins-->Configure System-->E-mail Notification.

![image](https://user-images.githubusercontent.com/62610706/137866204-02738b93-9d8e-41cb-a835-a41a167b307b.png)

Now,Email will be sent for every build by the choosing Always in the Default Triggers.

![image](https://user-images.githubusercontent.com/62610706/137866285-40ff679f-1ce5-44e2-8f86-d19d1c2b7423.png)

4. Create One extra job  for monitor : If container where app is running. fails due to any reason then this job should automatically start the container again from where the last trained model left.
![image](https://user-images.githubusercontent.com/62610706/137866383-cf79d0ca-c462-4528-8fb0-c24c5239ebf3.png)

![image](https://user-images.githubusercontent.com/62610706/137866411-c31f6299-07a2-45ab-9013-1cda5f712a37.png)


check.py - https://github.com/asthagoel01/trying.git (Written by me)
tweak.py- https://github.com/asthagoel01/trying.git (Written by me)
FinalModel.py - https://github.com/asthagoel01/mlt3.git (Refrenced at some places)
