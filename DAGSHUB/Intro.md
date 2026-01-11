- DagsHub is basically used for remote repositories

## DagsHub is a collaborative platform for data science and machine learning projects, somewhat like GitHub but tailored for ML workflows. It provides version control, experiment tracking, and collaboration features specifically designed for ML teams.

## Why is DagsHub used?

- 1. Version Control for Data & Models

Traditional GitHub works well for code but struggles with large datasets and model binaries.

DagsHub integrates Git + DVC (Data Version Control) to manage datasets and ML models efficiently.

- 2. Experiment Tracking

Integrates with MLflow to log experiments (hyperparameters, metrics, artifacts).

Makes comparing different ML runs easy.

- 3. Reproducibility

Ensures that anyone can reproduce results by combining code, data, and environment dependencies.

- 4. Collaboration

Just like GitHub, but designed for ML teams.

Teams can share datasets, trained models, pipelines, and experiments in one place.

- 5. Open Source Friendly

Many open-source ML projects use DagsHub because it provides free hosting and tracking for datasets, models, and experiments.

## What is a Remote Repository?

- A remote repository is just a version of your project that’s hosted on the internet (on a server), instead of your local machine.

- You can push changes from your computer to the remote repo, and pull updates made by others.

- Think of it as a central hub where code (and sometimes data/models) is stored, so multiple people can collaborate.

- Examples: GitHub, GitLab, Bitbucket → all are remote repositories for code.

## Why is DagsHub used as a Remote Repository?

## Unlike GitHub (which mainly handles code), DagsHub is designed for ML/Data Science projects. It lets you use a single remote repo for:

- Code (via Git) – Store and version control your Python/ML scripts.

- Data (via DVC / Git-LFS) – Store and version control datasets that are too large for Git.

- Models (via DVC / MLflow) – Save trained model weights alongside the code.

- Experiments (via MLflow) – Track metrics, hyperparameters, and results.

- Dagshub can be integrated with mlflow and DVC to track experiments and versions of the model.

## Difference between dagshub and github
In dagshub basically 3 main things are supported:
- Uploading data to dagshub , through this u will be able to track ur data by using DVC over here. (dagshub provides remote repository to upload some data -> around 10GB(available space) it uses S3 bucket).
- Helps to leverage git versioning of ur code , u can also track ur code over here.
- We can log experiments where we can basically use MLflow(we can run MLFlow tracking server here itself).

In github we can maintain only the version of our code -> but in dagshub we have 3 features as listed above.

## To get started with data we can configure our data storage
- Simple data upload(Upload data directly to DagsHub storage. Similiar to S3 or Google Drive. Simple and scaleable but not versioned).
- Versioned data upload(upload data to be managed by Git and DVC).
- Connect (connect an existing cloud storage bucket that already contains your data).

- In collaborations section in dagshub u can also collaborate with multiple peoples.
- In annotations u can : 1. Create a datasource 2. Select datapoints to annotate 3. Start annotating(imp for a Computer Vision Project)

- git clone https://dagshub.com/amritanshubhardwaj12crosary/demodagshub.git    -> git cloning the remote repository created in dagshub.
- In DAGSHUB folder we did cd MLOPS , then cd DVC and then their we git cloned it.
- after that cd demodagshub -> u will be in your cloned repository -> then do code. -> this will open u your vscode.

- in terminal git add README.md
- then git commit -m "first commit"

- Then we will create a branch which is main : git branch -M main
- Then push to this main branch : git push -u origin main

- Then when u will reload u will be able to see your first file in demodagshub which is README.md and the hashkey also their generated for the first commit.

## As told u had three things:
- Upload data to dagshub.
- Track your code. (U will see that this has got enabled(tick appearing) as u are tracking your code now using git)
- Log experiments

- In demodagshub create another folder data -> In that folder add diabetes dataset which is named as data.csv

- Our main aim is to track the versioning of the data.csv in the data folder

- 1. First we initialize dvc -> dvc init.
- 2. To want anything to be tracked by dvc -> dvc add data/data.csv (here we are tracking this particular file or dataset)
 After this in ur data folder u will be having like 3 things : ur original data.csv , data.csv.dvc , .gitignore
- 3. To track changes with git now as data.csv is already getting tracked by dvc we do git add data/data.csv.dvc and git add data/.gitignore
- 4. In data.csv.dvc , md5 has the data(in data.csv) represented as the hash key
- 5. We do git add data/.gitignore data/data.csv.dvc
- 6. Then git commit -m "Added data.csv with DVC"
- We are tracking all of these things with git and DVC so now we will push all of these things to our demodagshub repository
- How do we push it ??
- In dagshub when u open ur repo demodagshub , u will see a Remote button in green -> it will have 3 options : Code , data , experiments
- Since we our working with data we go in data , in data 2 options dagshub client and dvc , we go for dvc as we are working with dvc.
- Their is dvc we see that dagshub remote repository provides us with some bucket. -> all code for setup is available there.
- we need to setup our dagshub dvc remote where i need to store all my data information so that the versioning of that particular data will happen -> we need to configure it -> to configure it Use codes given in the Header Add a dagshub dvc remote: 
- dvc remote add origin s3://dvc -> this is where my entire data info will get stored.
- after this we will setup the endpoint url (all these commands are available their in remote -> data -> dvc -> Add a dagshub dvc remote(header))
- dvc remote modify origin endpointurl https://dagshub.com/amritanshubhardwaj12crosary/demodagshub.s3 -> code available there 
- dagshub dvc remote -> where all the data will be stored , all the versioning of the data information will be stored.
- We also need to setup our security credentials : 
- Code available in the same place as above just in header Setup Credentials 
- Avalible codes :
- dvc remote modify origin --local access_key_id 0fb168e7cb38689121e16da0859f210fbc442180 -> dvc remote is setup with the name origin , i.e. the remote name place where we are setting it up is origin.
- dvc remote modify origin --local secret_access_key 0fb168e7cb38689121e16da0859f210fbc442180  -> setting secret access key
- now if u do : dvc remote list -> to know how many remote lists u have. -> it is givng origin s3://dvc -> only list available
- then dvc pull -r origin -> what is the recent info that is present inside that dagshub repository will come out (make ensure library dvc-s3 is installed as because of this library only we are able to push and pull information) -> internally its using boto3 -> as it is S3 bucket itself -> 10GB space it provides.
- then dvc push -r origin -> pushing the changes in my local machine -> pushed to S3 bucket
- Final push : git push origin main -> git push origin to main
- Now if u go to dagshub and refresh it u will be able to see what all ur files(.dvc folder,data folder,.dvcignore,readme) have been pushed to the demodagshub repository. , dvc has got enabled , git has got enabled.
- U will also be able to see the datapipeline(in visualized form).-> automatic datapipeline has been created.(color scheme is also there indicating what it is).
- There in dagshub when u go to see the data.csv in the data folder u will be able to see its DVC.
- To see the history go to data.csv.dvc file there on the right top of the file there is a button of history , u will be able to see the history of commits. data.csv.dvc me hash key hai of the file stored. 
- in history u will be able to compare with the previous one, also u will be able to see the recent commit.
- total start to end history dekhne ke liye history me jaake click the message -> u will get complete status.

## What if i make some changes in the data ??
- Let's say u removed few records.
- Then update it -> dvc add data/data.csv
- when u do this 'M' icon in yellow will appear at data.csv.dvc saying that the file is modified, reason why its getting modified is that u are getting a new md5 hashkey(encrypted key) there -> hashkey changed as data is updated -> new hashkey is generated for new/updated data.
- Then do git add .
- then commit it -> git commit -m "Second Commit" -> here "Second Commit" is a message
- then dvc pull -r origin
- then dvc push -r origin -> pushing all the new information.
- then git push origin main
- second commit is also added -> then u go to data.csv.dvc in data , click history there u will be able to see all the commits done so far u will be able to track it , also u will be able to compare between multiple commits , these commits will have different sha1 -> keys.
- similarily u will also be able to see ur entire data.csv in the data folder.
- Now we have also uploaded the data to dagshub(dagshub remote) , along with tracking code previously.