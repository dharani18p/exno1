# Exno:1
Data Cleaning Process

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


            
# DATA CLEANING
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
data = pd.read_csv("/content/SAMPLEIDS.csv")
data.head()
```
![image](https://github.com/dharani18p/exno1/assets/118343366/b98aabc3-b953-4f60-91e6-db9366872870)

```
data = pd.get_dummies(data)
data.isnull().sum()
```

![image](https://github.com/dharani18p/exno1/assets/118343366/b18bdb7e-52fe-4730-bd0f-c5c38f731900)

```
columns_with_null = data.columns[data.isnull().any()]
import seaborn as sns
plt.figure(figsize=(10,10))
sns.barplot(columns_with_null)
plt.title("NULL VALUES")
plt.show()
```

![image](https://github.com/dharani18p/exno1/assets/118343366/2bdef3c5-465b-4273-86b7-8afd68554d4b)

```
for column in columns_with_null:
    median = data[column].median()  
    data[column].fillna(median, inplace=True)
data.isnull().sum().sum()
```
#IQR
```
import pandas as pd
import seaborn as sns
ir = pd.read_csv("/content/iris (1).csv")
ir.head()
```

![image](https://github.com/dharani18p/exno1/assets/118343366/e5abefc9-d6ee-468c-9d9b-459423d32ae0)

```
ir.describe()
```

![image](https://github.com/dharani18p/exno1/assets/118343366/b1a845ae-c98b-43e0-984c-3f15837c33ce)

```
sns.boxplot(x='sepal_width',data=ir)
```
![309135615-3b4d7891-2bb0-4c00-a5f4-02e0be6035f6](https://github.com/dharani18p/exno1/assets/118343366/0f2e9c08-73e8-4b6c-ae72-5dca7d7f6eb8)

```
c1=ir.sepal_width.quantile(0.25)
c3=ir.sepal_width.quantile(0.75)
iq=c3-c1
print(c3)
```
![309135740-a525ca98-7554-4860-98cb-b417ec6f6de5](https://github.com/dharani18p/exno1/assets/118343366/02b52f29-ea35-4a7f-9710-c3577609d325)

```
rid=ir[((ir.sepal_width<(c1-1.5*iq))|(ir.sepal_width>(c3+1.5*iq)))]
rid['sepal_width']
```
![309135777-265bcde4-895d-4333-8226-7a2f24d6196d](https://github.com/dharani18p/exno1/assets/118343366/0db0d93f-6f43-45e0-be33-bc45db9d223b)

```
delid=ir[~((ir.sepal_width<(c1-1.5*iq))|(ir.sepal_width>(c3+1.5*iq)))]
delid
```

![image](https://github.com/dharani18p/exno1/assets/118343366/ce05481c-7358-4bbe-bc6e-d1f48be970ce)

```
sns.boxplot(x='sepal_width',data=delid)
```

![image](https://github.com/dharani18p/exno1/assets/118343366/ceb2beac-5914-4185-b6ae-92e73d17ed62)

```

# Z SCORE
```
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np
import scipy.stats as stats
dataset=pd.read_csv("/content/heights.csv")
dataset

```
![image](https://github.com/dharani18p/exno1/assets/118343366/34001513-e39f-4632-a69e-512ebc3d3f54)
```

df = pd.read_csv("heights.csv")
q1 = df['height'].quantile(0.25)
q2 = df['height'].quantile(0.5)
q3 = df['height'].quantile(0.75)
iqr = q3-q1
iqr
```

![image](https://github.com/dharani18p/exno1/assets/118343366/05729194-0607-42d7-8126-0d4bbb64effc)

```
low = q1 - 1.5*iqr
low
```

![image](https://github.com/dharani18p/exno1/assets/118343366/3b25c954-b1a7-4c07-930c-8d47bc42c6c0)

```
high = q3 + 1.5*iqr
high
```

![image](https://github.com/dharani18p/exno1/assets/118343366/dbb2ffd4-1226-487f-a508-7ea5ae3d4128)


```
df1 = df[((df['height'] >=low)& (df['height'] <=high))]
df1
```

![image](https://github.com/dharani18p/exno1/assets/118343366/74406bf5-8682-4eca-b5d5-b88a48fb45a1)

```
z = np.abs(stats.zscore(df['height']))
z
```

![image](https://github.com/dharani18p/exno1/assets/118343366/36d16b41-3aab-47ee-bd51-0d6a9904d5a2)
```



# Result
Thus the outliers are detected and removed in the given file and the final data set is saved into the file.       
