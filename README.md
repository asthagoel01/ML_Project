# ML_Project
What is the Purpose of this Project?
We make Model in ML so we can find a formula using experiences.Here,we also made some Model but The Accuracy of the Model really matters a lot because in today's world ,almost everything is dependent on Machine auto Intelligence(comes from the Model) and so the correctness of the Model matters alot.

But it becomes hectic to make a good model because of many hyperparamaters(parameters which we need to set by own) so as to acheive good Accuracy and takes Much Time.

But in today's world,we have became much dependent on machines that we can't wait much ,also can't do such manual things in machine;s world.

So,here I tried toautomate the process of changing hyperparameters.Although there are many hyperparameters we need to change to acheive Wished accuracy;

But here I tried to automate the setting of No. of neurons.

Less Neurons becomes insufficient for traning and making general formula ,in short, good model can't be acheived.

More Neurons do Overfiiting,means learn dataset or a same pattern so Model not expertise on different-different patterns.

Hereare steps for my task.
Create container image that’s has Python3 and Keras or numpy installed using dockerfile.
When we launch this image, it should automatically starts train the model in the container.

2. Create a job chain of job1, job2, job3, job4 and job5 using build pipeline plugin in Jenkins.

 Job1 : Pull the Github repo automatically when some developers push repo to Github.
Job2 : By looking at the code or program file, Jenkins should automatically start the respective machine learning software installed interpreter install image container to deploy code and start training( eg. If code uses CNN, then Jenkins should start the container that has already installed all the softwares required for the cnn processing).
Job3 : Train your model and predict accuracy or metrics.
Job4 : if metrics accuracy is less than 80% , then tweak the machine learning model architecture.
Job5: Retrain the model or notify that the best model is being created.
3. Create One extra job job6 for monitor : If container where app is running. fails due to any reason then this job should automatically start the container again from where the last trained model left.

1. Create container image that’s has Python3 and Keras or numpy installed using the Dockerfile.

![image](https://user-images.githubusercontent.com/62610706/137864714-e86b98e3-36da-4fb8-82d6-5692b6c844a8.png)


The Dockerfile for image t3:v1.

Code for Model is in this FinalModel.py ,this file will be pushed by the Developer.The code will be pushed to remote repository.
![image](https://user-images.githubusercontent.com/62610706/137864774-5f3ad5de-5fc3-412e-b5ed-d8390c93e2be.png)
The Remote Repository is mlt3 github repo.
![image](https://user-images.githubusercontent.com/62610706/137864874-a6244082-9ee0-46a8-8e5e-ca0b0db34cdd.png)
The github link for Reference is:

https://github.com/asthagoel01/mlt3.git

Now,code present on Remote repository https://github.com/asthagoel01/mlt3.git will be triggered using Poll SCM trigger so that,updates will be there in Every seconds.
![image](https://user-images.githubusercontent.com/62610706/137864944-94e12852-8ae4-4f49-b864-cff12e597dab.png)
![image](https://user-images.githubusercontent.com/62610706/137864985-0729a48c-86c3-4c6a-b169-7cccbd0d05fa.png)
Output for the program;
![image](https://user-images.githubusercontent.com/62610706/137865050-2d7d497b-bb93-4039-b937-bf9c090bcb34.png)

Job2 : By looking at the code or program file, Jenkins should automatically start the respective machine learning software installed interpreter install image container to deploy code and start training( eg. If code uses CNN, then Jenkins should start the container that has already installed all the softwares required for the cnn processing).

Now,We run check.py file where we read the file in which code for model is written and if word convD is found anywhere then CNN will be printed which shows that it is CNN model.
So,now the Model will run in a docker container using image t3:v1, containing all the libraries for CNN model are present.
![image](https://user-images.githubusercontent.com/62610706/137865154-76510f6e-0777-4d40-ae7c-a344d5f7ff86.png)

![image](https://user-images.githubusercontent.com/62610706/137865185-726b0fb6-31c7-40d3-989f-5b1cdc77c109.png)

The file to check whether the code for the CNN Model is check.py.

The Reference for file is:https://github.com/asthagoel01/trying.git.

![image](https://user-images.githubusercontent.com/62610706/137865261-97324938-334f-4bbb-ac82-5598c0d1a8a9.png)
![image](https://user-images.githubusercontent.com/62610706/137865314-a4dce45c-7bb9-4426-bc8f-938f9ee6c9a0.png)
![image](https://user-images.githubusercontent.com/62610706/137865337-e99091b3-f611-4ef4-9aa1-bbb3549ed2e1.png)
![image](https://user-images.githubusercontent.com/62610706/137865362-13b759ed-5ac7-41d7-a488-248c8d4674b1.png)
6. Job3 : Train your model and predict accuracy or metrics.

Now,the docker container will be restarted in which Model was trained using FinalModel.py in t3j2 so that accuracy of the Model can be seen.

![image](https://user-images.githubusercontent.com/62610706/137865442-2adf71fe-f128-4026-bf68-c53e62fc9914.png)
![image](https://user-images.githubusercontent.com/62610706/137865482-f0e1505a-b704-496e-a9af-40c38f7f9311.png)
![image](https://user-images.githubusercontent.com/62610706/137865504-44163166-f8d2-4abc-9049-344b3c707557.png)
Job4 : if metrics accuracy is less than 80% , then tweak the machine learning model architecture.

Job5: Retrain the model or notify that the best model is being created.

Here, I made a new folder pre.In this,I copied file pushed by developer present in T3Job1 workspace.Developer pushed FinalModel.py file.Also there's code to write a text file(contain accuracy of the model) is also written in FinalModel.py file.So, I am copying both files(python and text) into the pre folder.

So,I restarted docker container in which FinalModel.py was run in t3j2 so that,the text file stored in Docker Container can be accessed and accuracy of the Model can be shown.

Now I also have another tweak.py file in my RHEL8 to tweak the Model in order to increase the Accuracy of the Model.

If the Accuracy of model is not 0.99 or 99%,then we will run tweak.py file in a new docker container using image that has interpreter installed already,so that 99% Acurracy can be acheived.
![image](https://user-images.githubusercontent.com/62610706/137865603-cadb9d55-b34c-4ca8-9aef-b253a8ba81bc.png)

![image](https://user-images.githubusercontent.com/62610706/137865630-5c697118-4688-4eed-bfe7-5a228763a2cb.png)
The file tweak.py is used to improve the Accuracy Model if the Accuracy of Model isn't 99% or 0.99.

Reference for this file(tweak.py):https://github.com/asthagoel01/trying.git.I used this file direct by RHEL8.I uploaded it on Github just for Reference.
![image](https://user-images.githubusercontent.com/62610706/137865723-3b949e20-d730-4b4c-8ed3-f5064928e207.png)

Now,After comparing Accuracy,the Accuracy was found 0.9746 so,now tweak.py file will run to improve the accuracy of Model by increasing No. of Neurons in every turn until 99% Accuracy acheived.

But,Sometimes ,more no. of neurons do overfitting(because more neurons,learn pattern of dataset and fails for the new images).So,inside the tweak.py file ,I compares last accuracy with current and If current Accuracy is less than Previous Accuracy so,further model will not train and loop will be exited so that Best Accuracy(Previous Accuracy) will be shown.

![image](https://user-images.githubusercontent.com/62610706/137865803-ec2b0882-09c4-43f9-ae24-76c537f0af74.png)

![image](https://user-images.githubusercontent.com/62610706/137865830-7a3bad27-f616-4505-a89d-3cafc6aaad73.png)

![image](https://user-images.githubusercontent.com/62610706/137865854-9b91d860-45dd-45db-ba5e-787e3a0be0b0.png)
![image](https://user-images.githubusercontent.com/62610706/137865913-10109004-6132-4211-b2c9-1cb6bc4d1cea.png)
![image](https://user-images.githubusercontent.com/62610706/137865941-d729efeb-f5cb-4546-93a2-334a93fbdc42.png)

![image](https://user-images.githubusercontent.com/62610706/137866000-8194a8cb-9d71-4209-afaf-2dded1169af8.png)
![image](https://user-images.githubusercontent.com/62610706/137866042-8f594c6a-0c03-4f05-8e21-bf90a9914d84.png)

On Best Accuracy Acheived ,mail will be sent to the Developer.

![image](https://user-images.githubusercontent.com/62610706/137866129-678de41a-32f0-4d5c-b92d-6b5f3f469b31.png)
NOTE:

For Successfully sending email,I used email-extension plugin.After installing the plugin,we need to do these things also in Manage Plugins-->Configure System-->E-mail Notification.



![image](https://user-images.githubusercontent.com/62610706/137866204-02738b93-9d8e-41cb-a835-a41a167b307b.png)

Now,Email will be sent for every build by the choosing Always in the Default Triggers.

![image](https://user-images.githubusercontent.com/62610706/137866285-40ff679f-1ce5-44e2-8f86-d19d1c2b7423.png)

9. Create One extra job job6 for monitor : If container where app is running. fails due to any reason then this job should automatically start the container again from where the last trained model left.
![image](https://user-images.githubusercontent.com/62610706/137866383-cf79d0ca-c462-4528-8fb0-c24c5239ebf3.png)

![image](https://user-images.githubusercontent.com/62610706/137866411-c31f6299-07a2-45ab-9013-1cda5f712a37.png)