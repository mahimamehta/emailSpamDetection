# emailSpamDetection

![image](https://user-images.githubusercontent.com/81260164/167015626-497d7e23-b9cb-4fb0-b1c5-9e09effc7ac1.png)


Outline:

1. Implement a Machine Learning model for predicting whether an SMS message is spam or not.
  a. Follow the following AWS tutorial on how to build and train a spam filter machine learning model using Amazon SageMaker: https://github.com/aws-samples/reinvent2018-srv404-lambda-sagemaker/ blob/master/training/README.md
  b. The resulting model should perform well on emails as well, which is what the rest of the assignment will focus on.
  c. Deploy the resulting model to an endpoint (E1).
2. Implement an automatic spam tagging system.
  a. Create an S3 bucket (S1) that will store email files.
  b. Using SES, set up an email address, that upon receipt of an email it stores it in S3.
      i. Confirm that the workflow is working by sending an email to that email address and seeing if the email information ends up in S3.
  c. For any new email file that is stored in S3, trigger a Lambda function (LF1) that extracts the body of the email and uses the prediction endpoint (E1) to predict if the email is spam or not.
      i. You might want to strip out new line characters “\n” in the email body, to match the data format in the SMS dataset that the ML model was trained on.
  d. Reply to the sender of the email with a message as follows:
  
      “We received your email sent at [EMAIL_RECEIVE_DATE] with the subject [EMAIL_SUBJECT].
      Here is a 240 character sample of the email body:
      [EMAIL_BODY]
      The email was categorized as [CLASSIFICATION] with a [CLASSIFICATION_CONFIDENCE_SCORE]% confidence.”
  
    i. Replace each variable “[VAR]” with the corresponding value from the email and the prediction.

    ii. The purpose of this step is to facilitate easy testing.
  
3. Create an AWS CloudFormation template for the automatic spam tagging system.
  a. Create a CloudFormation template (T1) to represent all the infrastructure resources (ex. Lambda, SES configuration, etc.) and permissions (IAM policies, roles, etc.).
  b. The template (T1) should take the prediction endpoint (E1) as a stack parameter.
