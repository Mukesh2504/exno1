# Exno:1
# Data Cleaning Process

# AIM
To read the given data and perform data cleaning and save the cleaned data to a file.

# Explanation
Data cleaning is the process of preparing data for analysis by removing or modifying data that is incorrect ,incompleted , irrelevant , duplicated or improperly formatted. Data cleaning is not simply about erasing data ,but rather finding a way to maximize datasets accuracy without necessarily deleting the information.

# Algorithm
STEP 1: Read the given Data

STEP 2: Get the information about the data

STEP 3: Remove the null values from the data

STEP 4: Save the Clean data to the file

STEP 5: Remove outliers using IQR

STEP 6: Use zscore of to remove outliers

# Coding and Output
```
Name: MUKESH A
Reg.no: 212223040118
```
# Data Cleaning
```py
import pandas as pd
df=pd.read_csv("/content/SAMPLEIDS.csv")
df
```
![Screenshot 2025-03-04 105641](https://github.com/user-attachments/assets/9a8a9cd4-9cb4-4536-9b6c-ae07a1e7949c)

```py
df.isnull().sum()
```
![Screenshot 2025-03-04 110231](https://github.com/user-attachments/assets/f6c8fe24-504b-45cd-89ed-509ebdd61bab)

```py
df.isnull().any()
```
![Screenshot 2025-03-04 110439](https://github.com/user-attachments/assets/139cf82c-3b9f-4290-9f4f-197a41b98f07)

```py
df.dropna()
```
![Screenshot 2025-03-04 110524](https://github.com/user-attachments/assets/f1b52c5f-ca88-4954-9237-a804dccfa988)

```py
df.fillna(0)
```
![Screenshot 2025-03-04 110712](https://github.com/user-attachments/assets/5003c5f3-e828-404b-96a3-ceeb7fbd6cce)


```py
df.fillna(method="ffill")
```
![Screenshot 2025-03-04 110751](https://github.com/user-attachments/assets/893658fb-1788-45a4-8d18-3fcb77ef037e)


```py
df.fillna(method="bfill")
```
![Screenshot 2025-03-04 110845](https://github.com/user-attachments/assets/1b58af05-839c-4e6a-a43a-8f1ed7fa9b11)

```py
df_dropped = df.dropna()
df_dropped
```
![Screenshot 2025-03-04 111147](https://github.com/user-attachments/assets/396013ab-a98c-4c1d-ab13-a81932ebd910)

```py
df.fillna({'NAME':'SAM','GENDER':'MALE','ADDRESS':'TAMBARAM','M1':80.0,'M2':85.,'M3':87.0,'M4':88.0,'TOTAL':340.0,'AVG':85.00})
```
![Screenshot 2025-03-04 111246](https://github.com/user-attachments/assets/ba66caf9-531f-4faa-a819-c463e7b5fc90)


# IQR(Inter Quartile Range)

```py
ir=pd.read_csv("/content/iris.csv")
ir
```
![Screenshot 2025-03-04 111415](https://github.com/user-attachments/assets/7508618d-153c-4365-89fb-733f1c598b98)


```py
ir.describe()
```
![Screenshot 2025-03-04 111451](https://github.com/user-attachments/assets/a8bd13ba-57a4-404f-ae32-193d1107bd20)


```py
import seaborn as sns
sns.boxplot(x='sepal_width',data=ir)
```
![Screenshot 2025-03-04 111622](https://github.com/user-attachments/assets/0d65b377-934e-4d32-a204-59e69fe1314e)


```py
c1=ir.sepal_width.quantile(0.25)
c3=ir.sepal_width.quantile(0.75)
iqr=c3-c1
print(iqr)
```
![Screenshot 2025-03-04 111719](https://github.com/user-attachments/assets/0afe1f47-05ca-4422-a3f7-f96293d32849)


```py
rid=ir[((ir.sepal_width<(c1-1.5*iqr))|(ir.sepal_width>(c3+1.5*iqr)))]
rid['sepal_width']
```
![Screenshot 2025-03-04 111938](https://github.com/user-attachments/assets/9e7e3406-7967-41c4-b5fd-0c19157ca609)


```py
delid=ir[~((ir.sepal_width<(c1-1.5*iqr))|(ir.sepal_width>(c3+1.5*iqr)))]
delid
```
![Screenshot 2025-03-04 112057](https://github.com/user-attachments/assets/bb2b0e93-be6f-4bd4-8a45-b5e6cbdab04e)


```py
sns.boxplot(x='sepal_width',data=delid)
```
![Screenshot 2025-03-04 112151](https://github.com/user-attachments/assets/367fc8c1-2b80-4e89-9115-55b29639f6f9)

# Z-Score

```py
import matplotlib.pyplot as plt
import scipy.stats as stats

dataset=pd.read_csv("/content/heights.csv")
dataset
```
![Screenshot 2025-03-04 112420](https://github.com/user-attachments/assets/a7b7e6ce-772f-4181-8f0f-4b9d08b3e374)


```py
dataset = pd.read_csv("heights.csv")
q1 = dataset['height'].quantile(0.25)
q2 = dataset['height'].quantile(0.5)
q3 = dataset['height'].quantile(0.75)

iqr = q3-q1
iqr
```
![Screenshot 2025-03-04 112531](https://github.com/user-attachments/assets/7b7cc8fa-8f95-4754-8c75-1cc59c422214)

```py
low = q1- 1.5*iqr
low
```
![Screenshot 2025-03-04 112704](https://github.com/user-attachments/assets/1de2579d-efe5-4dd8-bf85-da76cd602b54)

```py
high = q3 + 1.5*iqr
high
```
![Screenshot 2025-03-04 112807](https://github.com/user-attachments/assets/6bca495b-825d-404c-b115-ed136297eb41)

```py
dataset1 = dataset[((dataset['height'] >=low)& (dataset['height'] <=high))]
dataset1
```
![Screenshot 2025-03-04 112924](https://github.com/user-attachments/assets/14a2472b-e96b-4a15-b079-9af909e40d52)

```py
z = np.abs(stats.zscore(dataset['height']))
z
```
![Screenshot 2025-03-04 113034](https://github.com/user-attachments/assets/86e19d5e-19c7-41a8-b37c-33ada476f39c)

```py
dataset1 = dataset[z<3]
dataset1
```
![Screenshot 2025-03-04 113123](https://github.com/user-attachments/assets/63282922-4b4e-4bd3-af63-6a2bb7f572ba)

# Result
Thus the data is cleaned and Outlayer is detected and removed using IQR and Z-score method.
