# Google Cloud Platform

## Work Instruction Building Apps on GCP

We will use several step for configuration this project and provision :
1.	Compute Engine as a back-end
2.	Cloud SQL
3.	Cloud Storage
4.	App Engine as a Front-end

And in this project, we using lifecycle management for cloud storage.

This is the architecture what we want to build on GCP.
<br> ![Capture](Material/1.jpg) <br>

Now, lets do it,

1. Go to compute engine option, enable and create a VM
<br> ![Capture](Material/2.png) <br>
<br> ![Capture](Material/3.png) <br>

2. Follow this option to create the vm one.
<br> ![Capture](Material/4.png) <br>

3. And select what OS you want. In this project am using Ubuntu 20.04.
<br> ![Capture](Material/5.png) <br>
<br> ![Capture](Material/6.png) <br>

4. In the firewall option, select “Allow HTTP traffic” and Allow HTTPS traffic”. Then click create.
<br> ![Capture](Material/7.png) <br>

5. Wait for a few second, and vm was run.
<br> ![Capture](Material/8.png) <br>

6. Next we setup cloud sql as database for this back-end service. Create a instance.
<br> ![Capture](Material/9.png) <br>

7. Choose mysql for databases.
<br> ![Capture](Material/10.png) <br>

8. Fill some info about the instance.
<br> ![Capture](Material/11.png) <br>

9. Choose region just single zone.
<br> ![Capture](Material/12.png) <br>

10. In customize instance, choose machine type like this.
<br> ![Capture](Material/13.png) <br>

11. And for storage, choose HDD.
<br> ![Capture](Material/14.png) <br>

12. And then, click create instance.
<br> ![Capture](Material/15.png) <br>

13. The sql instance was created. Then go to connection option.
<br> ![Capture](Material/16.png) <br>

14. Click “Add Network”.
<br> ![Capture](Material/17.png) <br>

15. Fill the name and CIDR like this and click done.
<br> ![Capture](Material/18.png) <br>

16. And save the network.
<br> ![Capture](Material/19.png) <br>

17. Now we will connect the sql instance to vm instance was we created before. Save the ip address from sql instance.
<br> ![Capture](Material/20.png) <br>

18. Then go to the vm instance. And open ssh cloud shell. Run “sudo apt-get update”
<br> ![Capture](Material/21.png) <br>

19. And then run “sudo apt-get install mysql-client”
<br> ![Capture](Material/22.png) <br>

20. If the mysql-client done to install, then we connect the sql one to vm. Run command like this (input the sql instance ip address).
<br> ![Capture](Material/23.png) <br>

21. Now we create new database.
<br> ![Capture](Material/24.png) <br>

22. And create table from the database. Use this command to create.
<br> ![Capture](Material/25.png) <br>
<br> ![Capture](Material/26.png) <br>

23. Run “show tables” to see the table of database.
<br> ![Capture](Material/27.png) <br>

24. Now the cloud sql instance and vm was connected. Next we configure cloud storage to save any media file from web input. Go to cloud storage and create a bucket.
<br> ![Capture](Material/28.png) <br>

25. Set the name of bucket.
<br> ![Capture](Material/29.png) <br>

26. And set the region.
<br> ![Capture](Material/30.png) <br>

27. Choose standar storage.
<br> ![Capture](Material/31.png) <br>

28. Set the default one.
<br> ![Capture](Material/32.png) <br>

29. And then create.
<br> ![Capture](Material/33.png) <br>

30. Now we was created the bucket of storage.
<br> ![Capture](Material/34.png) <br>

31. Now we config the back-end code before deploy to vm. I already have source code for back-end (disclaimer : this source code from dicoding), and then config. Config for TODO code imgUpload.js.
<br> ![Capture](Material/35.png) <br>

32. Config for TODO code record.js.
<br> ![Capture](Material/36.png) <br>

33. And then we create key for serviceaccountkey.json from google cloud platform. This key we use for acces gcs to create any object to there. Go to service account menu. And then click create service account.
<br> ![Capture](Material/37.png) <br>

34. Fill any requirement to the field.
<br> ![Capture](Material/38.png) <br>

35. Select role for this service. You can follow the below this capture. Then continue.
<br> ![Capture](Material/39.png) <br>

36. Just field Service account users role. Field your google cloud account who develop back-end program in compute engine (exp, user@gmail.com). Then click done.
<br> ![Capture](Material/40.png) <br>

37. You can see, the service account was created. Then we will create the key. Click the service account.
<br> ![Capture](Material/41.png) <br>

38. Go to the key, and click add key, then create new key.
<br> ![Capture](Material/42.png) <br>

40. Choose JSON and then click create.
<br> ![Capture](Material/43.png) <br>

41. You will noticed that the key was download to your local pc. Then use the key for your serviceaccountkey.json. just replace it.
<br> ![Capture](Material/44.png) <br>

42. Now go to compute engine. We will deploy back-end apps using node js. But before deployed, we must set this service account to the compute engine. So we must stop the vm then re-setting the service account.
<br> ![Capture](Material/45.png) <br>
<br> ![Capture](Material/46.png) <br>

43. Vm was stop. Now we re-setting the service account for this vm. Click the vm. Then click edit.
<br> ![Capture](Material/47.png) <br>

44. Scroll down until service account menu. And then choose service account was we created before. Then click save.
<br> ![Capture](Material/48.png) <br>

45. After we set it, then start the vm again. You can see vm was running.
<br> ![Capture](Material/49.png) <br>

46. Go to the vm, then following this command : 
    - sudo apt-get update
    - sudo apt-get install nodejs npm
    - sudo apt install git
<br> ![Capture](Material/50.png) <br>

47. Now we check npm dan node version was installed.
<br> ![Capture](Material/51.png) <br>

48. Now we deploy the back-end code in vm. I already have the code in this vm. You can download all the code from “https://github.com/teguhraisrahmadi/building-apps.git”. 
- Run this command to clone source code from github “git clone https://github.com/teguhraisrahmadi/building-apps.git --branch=back-end --single-branch”.
<br> ![Capture](Material/52.png) <br>

49. Go to the file.
<br> ![Capture](Material/53.png) <br>

50. Before we deploy the back-end program, we will set the firewall to allow acces from outside world to this vm. Right, go to vpc network firewall setting. Then click create firewall rule.
<br> ![Capture](Material/54.png) <br>

51. Fill the name and description.
<br> ![Capture](Material/55.png) <br>

52. Scroll down, then choose targets to Specified service account. Then choose Target service account to service account was we created. 
<br> ![Capture](Material/56.png) <br>

53. Fill source IPv4 ranges to 0.0.0.0/0. For protocol choose TCP and fill port 8000,8080,80.
<br> ![Capture](Material/57.png) <br>

54. Scroll down, then click create.
<br> ![Capture](Material/58.png) <br>

55. You can see, the firewall was created.
<br> ![Capture](Material/59.png) <br>

56. Now we back to compute engine, and deploy the back-end apps. Note, before we deployed the code, make sure you was replaced serviceaccountkey.json with new service account was we download before. If was, just following this command to deploy the back-end apps : 
    - npm install
    - npm run start
<br> ![Capture](Material/60.png) <br>

57. You can see the respone from “http://ip_public:8000”
<br> ![Capture](Material/61.png) <br>

58. The response was success that’s mean back-end program was success deployed. So, for the best experience tools, we use nginx for reverse proxy this server. Install the nginx,
    - “sudo apt-get install nginx”
<br> ![Capture](Material/62.png) <br>

59. Go to /etc/nginx/conf.d directory. Then create file backend.conf.
<br> ![Capture](Material/63.png) <br>

60. Then write this configuration.
<br> ![Capture](Material/64.png) <br>

61. Now we test the nginx configuration file. If success, then reload the nginx service.
<br> ![Capture](Material/65.png) <br>

62. You can see, it was success acces the back-end program without write the 8000 port.
<br> ![Capture](Material/66.png) <br>

63. For the best experience running back-end, we use pm2 for process manager. Now we install the pm2 in the back-end directory.
    - sudo npm install –g pm2
<br> ![Capture](Material/67.png) <br>

64. You can start your program just run this command :
    - pm2 start app.js
<br> ![Capture](Material/68.png) <br>

65. And you can stop the program just run this command : 
    - Pm2 stop app.js
<br> ![Capture](Material/69.png) <br>

66. You can see, when we run “pm2 start app.js”, back-end apps was success running on the vm.
<br> ![Capture](Material/70.png) <br>

67. Next step we will deploy the front-end apps to app engine. Go to app engine and click open In new window.
<br> ![Capture](Material/71.png) <br>

68. Open editor.
<br> ![Capture](Material/72.png) <br>

69. You can see the editor from cloud shell here. Then open new terminal.
<br> ![Capture](Material/73.png) <br>
<br> ![Capture](Material/74.png) <br>

70. Open the project :
    - “gcloud config set project [PROJECT_ID]”
<br> ![Capture](Material/75.png) <br>

71. I already have the front–end code. You can download all the code from “https://github.com/teguhraisrahmadi/building-apps.git”. Run this command to clone source code from github, 
    - “git clone https://github.com/teguhraisrahmadi/building-apps.git --branch=front-end --single-branch”.
<br> ![Capture](Material/76.png) <br>

72. Now, open the folder, and choose directory was we clone before.
<br> ![Capture](Material/77.png) <br>

73. Now we entered to the directory.
<br> ![Capture](Material/78.png) <br>

74. Got to : application -> config -> config.php. fill base url in todo code
<br> ![Capture](Material/79.png) <br>

75. application -> models -> Record_model.php. then fill the API url was we created on compute engine.
<br> ![Capture](Material/80.png) <br>

76. Save and deployed the front-end in app engine.
<br> ![Capture](Material/81.png) <br>

77. Now you can open the application from http://building-apps-dot-empirical-state-358113.et.r.appspot.com
<br> ![Capture](Material/82.png) <br>
<br> ![Capture](Material/83.png) <br>

78. You can add records for new insert data to the application. And you can choose file upload to gcs storage. Then click submit.
<br> ![Capture](Material/84.png) <br>

79. In records menu, you have new data was created.
<br> ![Capture](Material/85.png) <br>

80. You can click attachment to see the file.
<br> ![Capture](Material/86.png) <br>

Done, Thanks.
