# IPL-Data-Analysis by Apache Spark

Data source: <https://data.world/raghu543/ipl-data-till-2017/workspace/data-dictionary>

Things learned from this project

1.  Intro to Spark
2.  Databricks -free community version.
3.  Connect S3 bucket to Databricks using (public access)

# Databricks Account Setup

Create account with "Community Edition" for free access

## **Step 1: Create a cluster**

1.  Click **Compute** in the sidebar.

2.  On the Compute page, click **Create Cluster**. This opens the New Cluster page.

3.  Specify a unique name for the cluster, leave the remaining values in their default state, and click **Create Cluster**

For more documentation, refer: <https://docs.databricks.com/en/index.html>

## **Step 2: Create a Databricks notebook**

To get started writing and executing interactive code on Databricks, create a notebook.

1.  Click **New** in the sidebar, then click **Notebook**.

2.  On the Create Notebook page:

    -   Specify a unique name for your notebook.

    -   Make sure the default language is set to **Python** or **Scala**.

    -   Select the cluster you created in step 1 from the **Cluster** dropdown.

    -   Click **Create**.

# Making S3 bucket publicly accessible

Follow the steps below:

1.  **Sign in to the AWS Management Console:** Go to the Amazon S3 console at <https://console.aws.amazon.com/s3/>.

2.  **Select the bucket:** Click on the name of the bucket you want to make public.

3.  **Go to the Permissions tab:** In the bucket dashboard, navigate to the "Permissions" tab.

4.  Navigate to Block public access (bucket settings) \> edit : Uncheck "Block All public access", save changes

5.  **Now, SCROLL DOWN AND go to Bucket policy, edit and click on Policy generator:**

    1.  **Select Type of Policy: S3 bucket policy**
    2.  effect: Allow
    3.  Principal : \* (as we want to allow all access)
    4.  Action: select "get object"
    5.  **Amazon Resource Name (ARN): select "Bucket ARN" from bucket policy page, example: "**arn:aws:s3:::xyz"
    6.  Click on add statement
    7.  Generate Policy

6.  Paste the generated policy on Policy generator page

7.  **Note: Make sure to add "/\*" at the end of Resource in policy**

    example:

    ```         
    "Resource": "arn:aws:s3:::abcabca/*"
    ```

8.  Save changes and done

# Best practices

1.  Always create your own schema first so that data types doesn't change in your data.
2.  Cluster pauses, if it is idle for more than 60 min. so pause it when not in use. Terminating sessions when they're not in use can help optimize resource usage and reduce costs, especially in cloud environments where resources are billed based on usage.
