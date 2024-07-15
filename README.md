# Ansible Refactoring & Static Assignments (Imports and Roles)
In this project, we will continue working with ansible-config-mgt repository and make some improvements of our code. Now we need to refactor our Ansible code, create assignments, 
and learn how to use the imports functionality. Imports allow to effectively re-use previously created playbooks in a new playbook - it allows us 
to organize our tasks and reuse them when needed.

## Step 1 - Jenkins job enhancement
Before we begin, let us make some changes to our Jenkins job - now every new change in the codes creates a separate directory which is not very convenient when we want to run some commands from one place. Besides, 
it consumes space on Jenkins serves with each subsequent change. Let us enhance it by introducing a new Jenkins project/job - we will require Copy Artifact plugin.

#### 1. Go to your Jenkins-Ansible server and create a new directory called ansible-config-artifact - we will store there all artifacts after each build.

Result:

<img width="938" alt="Screenshot 2024-07-15 at 17 21 01" src="https://github.com/user-attachments/assets/72004323-1888-47fd-8803-7c77a9097ebe">

```
sudo mkdir /home/ubuntu/ansible-config-artifact
```
Result:

<img width="841" alt="Screenshot 2024-07-15 at 17 22 09" src="https://github.com/user-attachments/assets/a3d573ab-b6ba-4028-969d-122c766b789e">

#### 2. Change permissions to this directory, so Jenkins could save files there

```
chmod -R 0777 /home/ubuntu/ansible-config-artifact
```

Result:

<img width="790" alt="Screenshot 2024-07-15 at 17 24 02" src="https://github.com/user-attachments/assets/f6c847bc-99d1-4616-a361-3ca2d46eb61c">

#### 3. Go to Jenkins web console -> Manage Jenkins -> Manage Plugins -> on Available tab search for Copy Artifact and install this plugin without restarting Jenkins

Result:

<img width="1678" alt="Screenshot 2024-07-15 at 17 27 09" src="https://github.com/user-attachments/assets/5964b449-31e4-440d-be98-aa1f0365e023">

<img width="1353" alt="Screenshot 2024-07-15 at 17 27 20" src="https://github.com/user-attachments/assets/51008c91-96e6-4165-94fd-a24a48c1c15d">

#### 4. Create a new Freestyle project and name it save_artifacts.

Result:

<img width="1660" alt="Screenshot 2024-07-15 at 17 28 51" src="https://github.com/user-attachments/assets/edb23f50-31c4-4b50-8e48-09187053431e">

#### 5. This project will be triggered by completion of your existing ansible project. Configure it accordingly

<img width="1646" alt="Screenshot 2024-07-15 at 17 30 51" src="https://github.com/user-attachments/assets/203f4493-706b-452d-8ee4-dcae527b8f8d">

**Note:** You can configure number of builds to keep in order to save space on the server, for example, you might want to keep only last 2 or 5 build results. You can also make this change to your ansible job.

#### 6. The main idea of save_artifacts project is to save artifacts into /home/ubuntu/ansible-config-artifact directory. To achieve this, create a Build step and choose Copy artifacts from other project, specify ansible as a source project and /home/ubuntu/ansible-config-artifact as a target directory.

Result:

<img width="1642" alt="Screenshot 2024-07-15 at 17 38 03" src="https://github.com/user-attachments/assets/53f4648a-dd84-4a30-aaba-79638c4ba5b9">

7. Test your set up by making some change in README.MD file inside your ansible-config-mgt repository (right inside main branch).

Result:

<img width="1442" alt="Screenshot 2024-07-15 at 17 41 14" src="https://github.com/user-attachments/assets/6b09c82a-a4dc-4d84-955b-ada6c29d2f44">

Remove the line - checking jenkins build

<img width="1677" alt="Screenshot 2024-07-15 at 17 42 38" src="https://github.com/user-attachments/assets/df88c35b-cdc4-4d65-96e9-e04d9033013f">

