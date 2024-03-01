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
### Data Cleaning
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
data = pd.read_csv("/content/SAMPLEIDS.csv")
data.head()
```

![1-1](https://github.com/Divya110205/exno1/assets/119404855/3ca587d6-9eab-4809-be07-6fecb7d38144)

```
data = pd.get_dummies(data)
data.isnull().sum()
```

![1-2](https://github.com/Divya110205/exno1/assets/119404855/5376ecdf-49bd-44cf-bfb0-c814590c8144)

```
columns_with_null = data.columns[data.isnull().any()]
import seaborn as sns
plt.figure(figsize=(10,10))
sns.barplot(columns_with_null)
plt.title("NULL VALUES")
plt.show()
```

![1-3](https://github.com/Divya110205/exno1/assets/119404855/b1022155-ea0a-4187-b06f-a78375303d43)

```
for column in columns_with_null:
    median = data[column].median()  
    data[column].fillna(median, inplace=True)
data.isnull().sum().sum()
```

![1-4](https://github.com/Divya110205/exno1/assets/119404855/c63d7324-1c97-49cb-a6a7-ecee861c386b)

### IQR
```
import pandas as pd
import seaborn as sns
ir = pd.read_csv("/content/iris (1).csv")
ir.head()
```

![1-5](https://github.com/Divya110205/exno1/assets/119404855/a12a23d1-ce37-46cc-9c29-f2df411b4170)

```
ir.describe()
```

![1-6](https://github.com/Divya110205/exno1/assets/119404855/0f478b80-2e6f-4115-acac-10468ed9b39c)

```
sns.boxplot(x='sepal_width',data=ir)
```

![1-7](https://github.com/Divya110205/exno1/assets/119404855/4eb55cb6-bf9f-47bf-8f97-c5a11edd0876)

```
c1=ir.sepal_width.quantile(0.25)
c3=ir.sepal_width.quantile(0.75)
iq=c3-c1
print(c3)
```

![1-8](https://github.com/Divya110205/exno1/assets/119404855/9e5ac1f7-f414-4799-bd30-be914233d1a3)

```
rid=ir[((ir.sepal_width<(c1-1.5*iq))|(ir.sepal_width>(c3+1.5*iq)))]
rid['sepal_width']
```

![1-9](https://github.com/Divya110205/exno1/assets/119404855/9765bd3c-5836-487b-8e81-564a8802aca9)

```
delid=ir[~((ir.sepal_width<(c1-1.5*iq))|(ir.sepal_width>(c3+1.5*iq)))]
delid
```

![1-10](https://github.com/Divya110205/exno1/assets/119404855/45fcdef3-e491-449b-afdc-c44153092c50)

```
sns.boxplot(x='sepal_width',data=delid)
```

![1-11](https://github.com/Divya110205/exno1/assets/119404855/69078496-2736-4ecd-9e19-e03d1738622b)

### Z SCORE
```
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np
import scipy.stats as stats
dataset=pd.read_csv("/content/heights.csv")
dataset
```

![1-12](https://github.com/Divya110205/exno1/assets/119404855/85a422ca-4fac-4db4-a32d-4a1508d736b8)

```
df = pd.read_csv("heights.csv")
q1 = df['height'].quantile(0.25)
q2 = df['height'].quantile(0.5)
q3 = df['height'].quantile(0.75)
```
```
iqr = q3-q1
iqr
```

![1-13](https://github.com/Divya110205/exno1/assets/119404855/264e6e9e-2f8b-47df-a3e8-33db992a783d)

```
low = q1 - 1.5*iqr
low
```

![1-14](https://github.com/Divya110205/exno1/assets/119404855/a80f4578-fc2b-4ca0-a524-6a05b12b8539)

```
high = q3 + 1.5*iqr
high
```

![1-15](https://github.com/Divya110205/exno1/assets/119404855/1a56212e-cc6f-40e8-80e0-2d918b356919)

```
df1 = df[((df['height'] >=low)& (df['height'] <=high))]
df1
```

![1-16](https://github.com/Divya110205/exno1/assets/119404855/7610c576-d3f6-4955-99b6-c0ec48183986)

```
z = np.abs(stats.zscore(df['height']))
z
```

![1-17](https://github.com/Divya110205/exno1/assets/119404855/29ca2a73-2b45-4de4-a538-0795024c5d55)

# Result
Thus the outliers are detected and removed in the given file and the final data set is saved into the file.
