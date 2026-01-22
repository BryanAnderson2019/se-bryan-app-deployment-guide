# Creating a monitoring dashboard
To start, head over to your instance's page, look for a tab called **Monitoring**, located below your instance's main information.
![An image of the instance page on the monitoring tab](guide_images/Dashboard/instance_page.png)

Now make sure that detailed monitoring is on by clicking on the **Manage detailed monitoring button**, you will be presented with a popup, click the **enable check box** then **confirm** to enable detailed monitoring.
![An image of the instance page on the monitoring tab](guide_images/Dashboard/Detailed_monitoring.png)
Detailed monitoring should be enabled as it keeps your monitoring data updated every minute.

Soon as you have enabled detailed monitoring, you can start creating your dashboard by first clicking the **3 dots icon** as shown below.
![An image of the instance page with the add to dashboard popup](guide_images/Dashboard/add_dashboard.png)
A **Add to dashboard** will show up below the icon, click the popup to be sent to the dashboard home page with a bigger **add to dashboard** popup.
![An image of the add to dashboard page](guide_images/Dashboard/create_dashboard_page.png)
When you click **create new**, you will need to give it a name before you can press **Create** and the **Add to dashboard button**.

Once you do Create a dashboard you will be presented with the dashboard page, allowing you to monitor your instance's data, like CPU usage.
![An image of a dashboard page](guide_images/Dashboard/dashboard_page.png)

# Create a CPU usage alarm
Now that you have a dashboard, you can create an alarm status. An alarm can be used to email you when a instance metric gose over a set threshold.

To start with, click on the **+ button**, this will open up the **Add widget** popup, chose the **Alarms** data type and click **next**.
![An image of the Add widget popup](guide_images/Dashboard/add_alarm.png)
You will be sent to the **Create alarm page** which requires you to do some steps to fully create your alarm.
![An image of the Create alarm page](guide_images/Dashboard/step1.png)

## Step 1. Specify metric and conditions
Start by clicking on the **Select metric button**, you will be presented with the **Select metric** popup.
![An image of the Select metric popup](guide_images/Dashboard/step1_select_metric.png)
There will be a lot of options but for this guide, we will be looking for the GPU usage of the sparta app instance. 

To get the GPU usage metric of a chosen instance, you will need to get its id, to do so, go back to your **instance's page** and copy the set of characters that starts with **i-...** as shown below.
![An image of a instance id](guide_images/Dashboard/instance_id.png)
Once you have the instance id, head back to the **Select metric** page and enter the id into the search bar: 
![An image of the Select metric popup with the instance id searched up](guide_images/Dashboard/step1_instance_search.png)
You will notice that only 2 options will be left, you will want to select the **EC2 > Per-Instance Metrics**.

Now you will just need to scrowl down on the list of metrics till you find the **CPUUtilization** metric, click on the check box and then the **Select metric button**.
![An image of the Select metric popup with the CPUUtilization metric selected](guide_images/Dashboard/step1_CPU.png)
A conditions popup should appear, here, you can chose what the threshold should be and when it should set off the alarm. I'm going to leave it as a **Static** threshold with the threshold value being 1. 
![An image of the Conditions popup](guide_images/Dashboard/step1_conditions.png)
Once you are happy with the settings, click the **Next** button to continue to the next step

## Step 2. Configure actions
Now that you have compleated stage one, you will now be presented with the notification settings. You can chose when you want notifications to be sent and where (what email).
![An image of the notification settings](guide_images/Dashboard/step2_create_topic.png)
You will need to create a topic if you have not done so before, all you need to do is give it a name and the email address that you want your alarm notifications to be seant to.
![An image of the notification settings filled in](guide_images/Dashboard/step2_topic_created.png)

If you need more than one email to be notified, you can click the **Add notification** button to add another topic to this alarm.
Once you are happy with the settings, click the **Next** button to continue to the next step

## Step 3. Add alarm details
In this step, you will be giving the alram a name, a description and any tags that can help you find or group alarms.
![An image of Add alarm details page](guide_images/Dashboard/step3.png)
At the very least, **you must give the alarm a name before you can continue**. Once you are ready, you can click the **Next** button to reach the final step.

## Step 4. Preview and create
This step lets you look back at all the steps and review if you are 100% happy with how the alarm has been set up. If there where any mistakes, you can always go back by clicking the **Previous** button to get back to a stage that needs attation before you create the alarm.
![An image of the Preview and create page](guide_images/Dashboard/step4.png)
If everything looks good, you can click on the **create** button. Your alarm should now be set up and be in the Cloudwatch system.

If you **created a topic**, you will need to first check your email(s) for an email by AWS Notification to confirm the subscription of the topic.
![An image my spam mail, as the AWS notifiaction email was sent there](guide_images/Dashboard/alarm_email.png)
You might need to check your **spam mail** for the subscription confirmation email.

![An image my AWS Notification - Subscription Confirmation email](guide_images/Dashboard/confirm_subscription.png)
Heres what the email should look like, you will need to click on the **Confirm subscriptions** link to start receaving emails when your alarm notifies you. ![An image my subscription being confirmed](guide_images/Dashboard/Subscription_confirmed.png)

# Example Alarm going off
At this stage, you should have a fully set up alarm. This section will showcase what happens when your alarm goes off.

With the alarm that I have set up, if the CPU usage goes over 1%, the alarm should go off and send me a notifaction through email.
![An image of my alarm page, In alarm](guide_images/Dashboard/graph_in_alarm.png)
In the image, you may notice that there will be an **!** mark next to the name of the alarm *(se-bryan-test-alarm)* and a little warning inside the graph on the top right *(In alarm)*.

On my Email, i have receaved an email by AWS Notifications letting me know that the state of the alarm has changed from **OK** to **ALARM**.
![An image of the AWS Notifcations ALARM email](guide_images/Dashboard/alarm_in_action.png)

# Deleting your dashboards and alarms
If you no longer need your dashboard or alarms any more, its easy to remove, and should be done to **reduce any costs**.

For your Dashboard, make sure you are on the correct dashboard page, then click on **Actions** and then **Delete dashboard**.
![An image of a dashboard page hovering over Delete dashboard](guide_images/Dashboard/Delete_dashboard.png)

For an alarm, go to the alarms page, then click on **Actions** and then **Delete**.
![An image of an alarm page hovering over Delete](guide_images/Dashboard/Delete_dashboard.png)

