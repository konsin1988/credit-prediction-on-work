# Predicting the integrity of bank clients
This project consists of two parts:
- Model development and training;
- Real time prediction

## Model development and training
#### Jupyter lab
In the first part, at the very beginning, we process the data and develop the model in jupyter lab. The data is stored in a container with a postgres database. We use pandas and catboost to process the data and obtain the model.

#### Mlflow (postgres and minio)
Next, we connect mlflow to our project (plus a container with postgres to store metrics and parameters and containers with minio to store model artifacts). Mlflow is very useful when you need to analyze models and compare one model with another.

#### Airflow (DockerOperator)
Our next goal is to automate the process of regular model training. To do this, we create a docker image, which, when launched, runs a script that receives new data and retrains the model. In airflow we use a docker operator that regularly runs a container from an image.

#### GitLab
Our final goal is to make it possible to improve the model when working together. For this, we use the CI/CD tool GitLab. We deploy GitLab using Docker on our server.

## Real time prediction
#### Streamlit
To visualize the user interface, we use a simple solution - streamlit. With its help, we create simple fields where you can enter data and below get the result in the form of a prediction of the client's integrity/dishonesty.

#### Fastapi
We use fastapi as a server part. Upon request, the model is loaded and a prediction is made, and the result flies to the frontend. The model is loaded from the minio s3 storage, where it goes after training.