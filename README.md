# Train local CIFAR-10 image classifier code with SageMaker training job

This repo contain the code to train a CIFAR-10 image classifier based on the [Pytorch Tutorial](https://pytorch.org/tutorials/beginner/blitz/cifar10_tutorial.html) using SageMaker training job. Further guide on running local code on SageMaker can be found [here](https://docs.aws.amazon.com/sagemaker/latest/dg/train-remote-decorator.html). 

## Setup

1. Create anaconda environment
    ```
    conda create -n local_code_sagemaker_job python=3.10 pip
    conda activate local_code_sagemaker_job
    ```
2. Install dependencies
    ```
    pip install -r requirements.txt
    ```

3. Edit settings in 'train.py' 
    ```
    sm_session = sagemaker.Session(boto_session=boto3.session.Session(region_name=<REGION>))
    settings = dict(
        sagemaker_session=sm_session,
        role=<IAM_ROLE_NAME>,
        instance_type=<INSTANCE_TYPE>,
        dependencies="auto_capture"
    )
    ```

3. Run the code
    ```
    python train.py
    ```

The function with `@remote(**settings)` decorator will be run on SageMaker training job. The rest of the code will be run locally.
