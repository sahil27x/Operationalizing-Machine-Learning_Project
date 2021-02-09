# Operationalizing Machine Learning

This project involves working with the [Bank Marketing Dataset](https://automlsamplenotebookdata.blob.core.windows.net/automl-sample-notebook-data/bankmarketing_train.csv). It includes model creation using Azure ML Studio, deploying it and then consuming the model through its API endpoints. Apart from that, it also includes creating a fully operational Machine Learning pipeline, publishing it as well as consuming it using Azure Python SDK.

## Architectural Diagram
The architecural diagram explains the flow of the project in a pictorial represenation. We start with installing the Azure az command line tool and create service principles(if we have our own subscription). We then create an Azure AutoML model using ML Studio and deploy the best model from the run. After enabling authentication, we enable Application Insights to maintain the logs of our model. We then use swagger to document model API structure, and thereafter consume the endpoints. We can also use Apache Benchmark tool for benchmarking the response, though it is not mandatory. Lastly, we publish a ML Pipeline using Azure Python SDK. 

The architectural diagram is not very detailed by nature; its purpose is to give a rough overview of the operations. The diagram below is a visualization of the flow of operations from start to finish:

<br></br> 
![alt text](https://github.com/sahil27x/Operationalizing-Machine-Learning_Project/blob/main/screenshot/ArchDia.png)


## Key Steps
#### 1. Registering the dataset in Azure ML Studio.<br></br>
Upload and register the bank marketing dataset to Azure ML studio datasets.
![alt text](https://github.com/sahil27x/Operationalizing-Machine-Learning_Project/blob/main/screenshot/dataset-avail.jpg)
<br></br>

#### 2. Creating the AutoML Model on the given dataset.<br></br>
Then, using Azure AutoML service, create an AutoML model that has to be deployed later. Use an existing compute, or create a new one. Increase the minimum number of nodes available to 1 and run the experiment. 
![alt text](https://github.com/sahil27x/Operationalizing-Machine-Learning_Project/blob/main/screenshot/automl-model-creation.jpg)
<br></br>

#### 3. VotingEnsembleClassifier is the best model.<br></br>
Select the best model on the data, which is usually the topmost and analyze the insights. Deploy this model and download the config.json file.
![alt text](https://github.com/sahil27x/Operationalizing-Machine-Learning_Project/blob/main/screenshot/best-model.jpg)
<br></br>

Deploying the best-model with Authenitication enabled using Azure Container Instance (ACI)
![alt text](https://github.com/sahil27x/Operationalizing-Machine-Learning_Project/blob/main/screenshot/deploy_model.jpg)
<br></br>

#### 4. Run the logs.py script to observe the logs.<br></br>
Write the code to enable application insights in the logs.py file and run the file. Observe the logs it provides of the deployed model.
![alt text](https://github.com/sahil27x/Operationalizing-Machine-Learning_Project/blob/main/screenshot/logsdotpy.jpg)
<br></br>

#### 5. Enable Application Insights for logging.<br></br>
You can see that the Application Insights which was earlier set to false, is now enabled.
![alt text](https://github.com/sahil27x/Operationalizing-Machine-Learning_Project/blob/main/screenshot/aienabled.jpg)
<br></br>

#### 6. Run the serve.py and swagger.sh files on localhost.<br></br>
Next we are going to use the swagger tool, which is a documentation and API structuring tool. For this we need Docker to be installed on the system as we need to download the container. Once docker is installed, run serve.py and swagger.sh file as shown.
![alt text](https://github.com/sahil27x/Operationalizing-Machine-Learning_Project/blob/main/screenshot/running-serve.py.jpg)
<br></br>
![alt text](https://github.com/sahil27x/Operationalizing-Machine-Learning_Project/blob/main/screenshot/running-swagger-container.jpg)
<br></br>
The swagger will be hosted locally on the port you have used in the above files.
![alt text](https://github.com/sahil27x/Operationalizing-Machine-Learning_Project/blob/main/screenshot/swagger-localhost.jpg)
<br></br>

#### 7. Swagger running on localhost.<br></br>
Since swagger is running locally now, we can see our model name as well as the API methods.
![alt text](https://github.com/sahil27x/Operationalizing-Machine-Learning_Project/blob/main/screenshot/swagger1.jpg)
<br></br>
Here you can see model name and API methods GET and POST.
![alt text](https://github.com/sahil27x/Operationalizing-Machine-Learning_Project/blob/main/screenshot/swagger-new1.jpg)
<br></br>
This is the service input payload.
![alt text](https://github.com/sahil27x/Operationalizing-Machine-Learning_Project/blob/main/screenshot/swagger2.jpg)
<br></br>
These are the responses that the deployed model sends from the endpoint.
![alt text](https://github.com/sahil27x/Operationalizing-Machine-Learning_Project/blob/main/screenshot/swagger-new2.jpg)
<br></br>

#### 8. Run the endpoint.py script to get JSON output from the model.<br></br>
The endpoint.py script sends a request to the deployed model via the POST API method and receives data in the form of JSON file which is displays. We have to set the scoring URI and the authentication key first. 
![alt text](https://github.com/sahil27x/Operationalizing-Machine-Learning_Project/blob/main/screenshot/endpoint.py.jpg)
<br></br>

#### 9. Pipeline is running in the Azure ML studio's pipeline section.<br></br>
The pipeline created through Azure Python SDK is now running in the portal.
![alt text](https://github.com/sahil27x/Operationalizing-Machine-Learning_Project/blob/main/screenshot/pipeline-running.jpg)
<br></br>

#### 10. Pipeline endpoint after publishing it.<br></br>
This is the published pipeline's endpoint 
![alt text](https://github.com/sahil27x/Operationalizing-Machine-Learning_Project/blob/main/screenshot/pipeline-endpoint.jpg)
<br></br>

#### 11. Bank Marketing Dataset with AutoML module. <br></br>
![alt text](https://github.com/sahil27x/Operationalizing-Machine-Learning_Project/blob/main/screenshot/pipeline-automl.jpg)
<br></br>

#### 12. Published Pipeline overview showing REST endpoint and Active Status. <br></br>
The published pipeline status is ACTIVE now and the REST endpoint is also available.
![alt text](https://github.com/sahil27x/Operationalizing-Machine-Learning_Project/blob/main/screenshot/activestatus.jpg)
<br></br>

#### 12. RunDetails Widget showing the step runs.  <br></br>
![alt text](https://github.com/sahil27x/Operationalizing-Machine-Learning_Project/blob/main/screenshot/jupyterrun.jpg)
<br></br>
Both the pipeline runs have been completed.
![alt text](https://github.com/sahil27x/Operationalizing-Machine-Learning_Project/blob/main/screenshot/scheduledrun1.jpg)
<br></br>


## Screen Recording
Click [here]() to see the ScreenCast.

## Scope of improvement:
Providing the option of enabling deep learning during AutoML model creation would prove beneficial in terms of results and learning. Cross-comparing the models on factors like scoring metric, computational complexity, running time can also be added. 
More focus can be given on benchmarking content and different tools can also be compared.

Although AutoML normally takes into account this imbalance automatically, there should be more room to improve the model's accuracy in predicting the minority class. For example, we could use Random Under-Sampling of majority class, or Random Over-Sampling of minority class, or even try different algorithms.
