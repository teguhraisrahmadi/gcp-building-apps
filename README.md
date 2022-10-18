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

10. 









