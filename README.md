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

39. Choose JSON and then click create.
<br> ![Capture](Material/41.png) <br>

40. You will noticed that the key was download to your local pc. Then use the key for your serviceaccountkey.json. just replace it.
<br> ![Capture](Material/43.png) <br>





























