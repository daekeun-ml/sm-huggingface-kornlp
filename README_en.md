# How to train and use a cloud-native Korean NLP model for everyone (Hugging Face meets Amazon SageMaker!)

There are many cases of AI/ML application of Natural Language Processing(NLP) such as text analysis, translation, sentence summarization, and entity classification, but many customers still have difficulties in adopting it due to technical barriers to entry. Some people are already accelerating the application of AIML with the Hugging Face transformer library and many example codes from SageMaker. However, until early 2021, SageMaker did not natively support containers for Hugging Face, so there was a difficulty in writing custom scripts and custom containers separately.

Recently, AWS introduced the Hugging Face Deep Learning Training Container and Inference Container, which makes it easier to train and deploy Hugging Face's transformer models on Amazon SageMaker. This enables rapid training and production deployment of NLP models with just a few lines of code without having to worry about setting up infrastructure.

This hands-on consists of training and reasoning part hands-on labs, each of which can be performed independently.

**_Note: Korean customers need sample code for Korean language models, not English models. Therefore, all of these Hands-Ons were written in Korean first. If you have a need for an English version, please contact the author._**

## Lab 1: Training

- **Training on Local Environment**: Reproduces the traditional method of training a Korean NLP model in an on-premises/local environment without calling the SageMaker API. If you are not familiar with Korean NLP and how to use the Hugging Face library, we recommend doing this hands-on.

- **Training on SageMaker**: You will learn how to train a Korean NLP model trained with Hugging Face in a cloud-native manner. Multi-GPU and multi-instance distributed training, including single-GPU based deep learning training, can be performed more easily and quickly because no additional work is required to set up the infrastructure.

## Lab 2: Serving

- **SageMaker Real-time Endpoint**: SageMakers provides a pre-built Hugging Face Inference container and Hugging Face Inference Toolkit, so you can proceed in the same way as you would with a traditional SageMaker endpoint deployment. In addition, you can learn how to deploy endpoints by directly importing models registered in Hugging Face Hub (https://huggingface.co/models) as a dedicated Hugging Face feature.

- **SageMaker Batch Transform**: SageMaker real-time endpoints can receive inference results in real time within a fast response speed, but at least one hosting server must be running, which is costly. In this case, you can use the SageMaker batch transform feature to save money by using compute instances only when performing batch transforms like training instances.

- **SageMaker Serverless Endpoint**: SageMaker Serverless Inference is a new inference option launched at re:Invent 2021 that is built to make it easy to deploy and scale models for Machine Learning without the burden of managing your hosting infrastructure. SageMaker Serverless Inference automatically starts compute resources and automatically scales in/out based on traffic, so you don't have to choose instance types or manage scaling policies. This makes it ideal for workloads that have idle periods between traffic spikes and can tolerate cold starts.


# References

- KoELECTRA: https://github.com/monologg/KoELECTRA
- Naver Sentiment Movie Corpus v1.0: https://github.com/e9t/nsmc
- Hugging Face on Amazon SageMaker: https://huggingface.co/docs/sagemaker/main
- Hugging Face examples: https://github.com/huggingface/notebooks/tree/master/sagemaker