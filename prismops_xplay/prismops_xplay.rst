------------------
Prism Ops - X-Play
------------------

Potential Use Cases (from Sarah's "Customer Requested Playbook Use Cases)
+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

Automatically adding memory/CPU on a constrained VM

   This can be achieved by cloning one of the Out of Box Playbooks in 5.11 and beyond. One of our largest customers is using this in production. Video Example https://youtu.be/Lqg7AjLtF4s

Automatically removing memory/CPU on an Overprovisioned VM

   This can be achieved by cloning one of the Out of Box Playbooks in 5.11 and beyond.

Manually adding/removing memory/CPU
   Sometimes it’s not practical to expect to be able to automate everything, but you can speed up manual sequences of actions by creating a manual trigger playbook and adding the sequence of actions there. Many of our customers are using this in the field today.

Automatically generate a Capacity Forecast Report when running out of runway
   This can be achieved by cloning one of the Out of Box Playbooks in 5.11 and beyond.

Take automated actions during a Maintenance Window
   This can be achieved by adding a wait action in your workflow to pause the playbooks execution until a defined window, such as 2AM Sunday. This is available in 5.11 and beyond.

Automate upgrades with LCM
   This can be achieved by using the REST API action to call the LCM REST API. REST API action has been available since 5.11. For the Trigger, in 5.17 a Time trigger will be released. This can then trigger the playbook at some defined interval to automatically start an upgrade.

Automatically expand disk space if it runs out
   This use case will become available in 5.17 release. Create a user defined Alert Policy to monitor the VM disk usage. When space is running out trigger a playbook on this alert, and use the Add/Expand disk actions.

Automatically send alerts to ServiceNow
   The ServiceNow action was added in 5.11.1, however it comes with a caveat. There is a 1-1 alert policy to playbook mapping in 5.11 meaning for each alert type a separate playbook is required. Paul Harb has generated a script for automating the creation of playbooks for all critical alerts. In 5.17, a trigger has been introduced to allow choosing multiple/all alerts for triggering a single Playbook. Many of our customers are using this today.

Service now can trigger automation inside Prism Pro
   This use case becomes available in 5.17 with the introduction of the webhook trigger. From service now you can hook up the actions you have taken (using the Flow Designer in SNOW to call to a specific webhook that triggers a Playbook. Useful for resolving initiating actions such as Add memory as well as Resolving alerts.

Manually put a Host into maintenance mode from the Prism Central UI
   Jarod Hallmark from Fariwaymc wrote a blog about this case http://hamsterlog.com/2020/02/13/creating-maintenance-mode-for-ahv-using-x-play/ It can be done in 5.11 and beyond. With PC.2020.8 this will become much simpler because we can look up the CVM IP address of the host using a REST query and the new String Parse action. Then it will make this playbook more dynamic and not need to have the CVM IP hard coded.

RUN NCC on Prism element
   Blog post http://vinception.fr/nutanix-run-ncc-on-multiple-clusters-with-prism-central-playbooks/

Use existing scripts with X-Play automation
   Host your existing scripts within a VM and then use the Powershell or SSH action to trigger these existing scripts. Available since 5.11.

Automatically queue up actions, but wait for manual approval before continuing
   This use case was introduced in 5.11. Using the Wait action and selecting the ‘And then ‘STOP’’ option. This means that the play execution will not resume on its own. A human must manually resume the play before the specified duration is up, otherwise it will be aborted.

Trigger LEAP Recovery Plan Test and send Results to email or send failures to ServiceNow
   From a POC we did.
      Requires 5.17.
      Playbook 1:
      Schedule Recovery Plan Test
      Using Time trigger it will schedule the test at some time
      Then it will call a REST API action to trigger the test
      Then we can trigger an SSH script in a VM that will initiate a process to poll the recovery plan test. From this script we will initiate the other playbooks depending on success or failure.
      Playbook 2:
      Email Results when successful
      Using the Webhook trigger, a script can call to this playbook on test success.
      It will have a REST API action to get the Report of the recovery plan.
      The response of the REST API will be included in an Email using the Email Action.
      Playbook 3:
      Create ServiceNow ticket when RP Test failure
      Using the Webhook trigger, a script can call to this playbook on failure.
      Using REST API, we can open a ticket with ServiceNow for the failure.

Automatically remove aged snapshots
   Using the alert for aged 3rd party snapshot detected, will then ssh in to the vm remove the snapshot, send an email and resolve the alert. A customer is using this in the field today.

Automatically Quarantine a VM
   Using some sort of alert or event (Example is a bully VM alert) we can then use a script to add that VM to the category to quarantine it. Alert version available since 5.11, event version available since 5.17.

Automate NGT installation
   Needs to be evaluated if there is a good way to do this, might be simpler for linux than windows. But this was requested in a recent customer call, we will look into it.

Send a message to Slack, Email, or even Microsoft Teams
   Many of our customers are using specifically the slack option to send alerts notifications out. We also get a ton of requests for MSTeams here is a video on how to do that. https://youtu.be/0TYhlKy70-4

Call to a calm blueprint
   Use any alert trigger (or manual trigger) as a trigger to the playbook. Then use the REST API action to call to the API to trigger a calm blueprint of your choice. This workflow has been available since 5.11.


Use Cases that still need to be thought through to find a solution
Auto Cleanup of 7 days old snapshots

Mark VMs for Deletion & delete during maintenance window

Auto generate capacity report for a set of clusters on a schedule
