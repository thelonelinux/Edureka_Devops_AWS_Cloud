# JENKINS JOBS AND SETTINGS (FAST FORWARD)

## Job Sequence
#### Always add username password when logging into jenkins as when you get logged off, you can easily login again. Else you won't be able to login again
###  1. addressbookCompile
* STEP 1: In Jenkins Click on (+) => name job as "addressbookCompile" => select freeStyleProject and then submit
* STEP 2: In the job configuration => add whatever description you like => In git select add this URL : https://github.com/htshshrm2/MyAddressbook.git =>/*Master only
* STEP 3: Since it's Java code, install Maven any version and name it as "myMaven"
* STEP 4: In job configuration again => In Prebuild select "Top Level Maven Target"  and then choose "mymaven" => There in job add this "compile".
* And then save it, it will be created.
* 
###  2. AddressbookCodeReview
* STEP 1: In Jenkins Click on (+) => name job as "AddressbookCodeReview" => select freeStyleProject and then submit
* STEP 2: In the job configuration => add whatever description you like => In git select add this URL : https://github.com/htshshrm2/MyAddressbook.git =>/*Master only
* STEP 3: Already done in the above step only, so there is no need to do it here again. (Since it's Java code, install Maven any version and name it as "myMaven")
* STEP 4: In job configuration again => In Prebuild select "Top Level Maven Target"  and then choose "mymaven" => There in the job add this "pmd:pmd".
* STEP 5: in Build Triggers: Build after another job is built => and add the previous job name after which this job has to be started, so here we add "addressbookCompile"
* And then save it, it will be created.
* 
###  3. addressbookUnittest
* STEP 1: In Jenkins Click on (+) => name job as "addressbookUnittest" => select freeStyleProject and then submit
* STEP 2: In the job configuration => add whatever description you like => In git select add this URL : https://github.com/htshshrm2/MyAddressbook.git =>/*Master only
* STEP 3: Already done in the above step only, so there is no need to do it here again. (Since it's Java code, install Maven any version and name it as "myMaven")
* STEP 4: In job configuration again => In Prebuild select "Top Level Maven Target"  and then choose "mymaven" => There in the job add this "test".
* STEP 5: in Build Triggers: Build after another job is built => and add the previous job name after which this job has to be started, so here we add "AddressbookCodeReview"
* And then save it, it will be created.
* 
###  5. addressbookMetrictest
* STEP 1: In Jenkins Click on (+) => name job as "addressbookMetrictest" => select freeStyleProject and then submit
* STEP 2: In the job configuration => add whatever description you like => In git select add this URL : https://github.com/htshshrm2/MyAddressbook.git =>/*Master only
* STEP 3: Already done in the above step only, so there is no need to do it here again. (Since it's Java code, install Maven any version and name it as "myMaven")
* STEP 4: In job configuration again => In Prebuild select "Top Level Maven Target"  and then choose "mymaven" => There in the job add this "cobertura:cobertura -Dcobertura.report.format=xml".
* STEP 5: in Build Triggers: Build after another job is built => and add the previous job name after which this job has to be started, so here we add "addressbookUnittest"
* STEP 6: Here we need jdk-8 to run, but we have jdk11 in our EC2 Server Instance. So we could have gone to Jenkins Manage and add jdk8 by giving HOME_PATH, but it didn't work, so follow below steps
  * $$ sudo apt install openjdk-8-jdk (Run this command to install jdk8 in our instance cli)
  * $$ sudo update-alternatives --config java (This checks which all java version are there, you can see jdk may be present in *2 location )
  * After you run this command you will get invoke to chose the default jdk-8 as default by typing 2 and enter.
  * $$ => Press to keep the current choice[*], or type selection number: 2
  * after this run again above command you will see our default will be *2 now where jdk-8 is present.
* And then save it, it will be created.
* 
###  6. addressbookPackage
* STEP 1: In Jenkins Click on (+) => name job as "addressbookPackage" => select freeStyleProject and then submit
* STEP 2: In the job configuration => add whatever description you like => In git select add this URL : https://github.com/htshshrm2/MyAddressbook.git =>/*Master only
* STEP 3: Already done in the above step only, so there is no need to do it here again. (Since it's Java code, install Maven any version and name it as "myMaven")
* STEP 4: In job configuration again => In Prebuild select "Top Level Maven Target"  and then choose "mymaven" => There in the job add this "package".
* STEP 5: in Build Triggers: Build after another job is built => and add the previous job name after which this job has to be started, so here we add "addressbookMetrictest"
* And then save it, it will be created.
* 
###  7. addressbookTomCatInstall          (Ansible Master/Slave) (PROD, UAT, QA )
###  8. addressbookDeployWar              (Ansible) (PROD, UAT, QA )
###  9. addressbookBuildImage             (Docker)
###  10. addressbookPushImage             (Docker)
###  11. addressbookDeployContainer       (Docker)
