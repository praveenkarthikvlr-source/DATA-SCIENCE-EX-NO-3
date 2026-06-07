## EXNO-3-DS

# AIM:
To read the given data and perform Feature Encoding and Transformation process and save the data to a file.

# ALGORITHM:
STEP 1:Read the given Data.

STEP 2:Clean the Data Set using Data Cleaning Process.

STEP 3:Apply Feature Encoding for the feature in the data set.

STEP 4:Apply Feature Transformation for the feature in the data set.

STEP 5:Save the data to the file.

# FEATURE ENCODING:
1. Ordinal Encoding
An ordinal encoding involves mapping each unique label to an integer value. This type of encoding is really only appropriate if there is a known relationship between the categories. This relationship does exist for some of the variables in our dataset, and ideally, this should be harnessed when preparing the data.

2. Label Encoding
Label encoding is a simple and straight forward approach. This converts each value in a categorical column into a numerical value. Each value in a categorical column is called Label.

3. Binary Encoding
Binary encoding converts a category into binary digits. Each binary digit creates one feature column. If there are n unique categories, then binary encoding results in the only log(base 2)ⁿ features.

4. One Hot Encoding
We use this categorical data encoding technique when the features are nominal(do not have any order). In one hot encoding, for each level of a categorical feature, we create a new variable. Each category is mapped with a binary variable containing either 0 or 1. Here, 0 represents the absence, and 1 represents the presence of that category.

# Methods Used for Data Transformation:
  # 1. FUNCTION TRANSFORMATION
• Log Transformation

• Reciprocal Transformation

• Square Root Transformation

• Square Transformation

  # 2. POWER TRANSFORMATION
• Boxcox method

• Yeojohnson method

# CODING AND OUTPUT:
import pandas as pd
df=pd.read_csv("/content/Encoding Data.csv")
df


# ORDINAL ENCODING
from sklearn.preprocessing import LabelEncoder,OrdinalEncoder
pm=['Hot','Warm','Cold']
e1=OrdinalEncoder(categories=[pm])
e1.fit_transform(df[["ord_2"]])


df['bo2']=e1.fit_transform(df[["ord_2"]])
df


 # Label Encoder ( orders in alphabetical order)
le=LabelEncoder()
dfc=df.copy()
dfc['ord_2']=le.fit_transform(dfc['ord_2'])
dfc


# ONE HOT ENCODING
from sklearn.preprocessing import OneHotEncoder
ohe=OneHotEncoder(sparse_output=False)
df2=df.copy()
enc=pd.DataFrame(ohe.fit_transform(df2[["nom_0"]])) # Orders in Alphabetical Order Blue , Green, Red
df2=pd.concat([df2,enc],axis=1)
df2


pd.get_dummies(df2,columns=["nom_0"])
image
pip install --upgrade category_encoders


from category_encoders import BinaryEncoder
df=pd.read_csv("/content/data.csv")
df



 be=BinaryEncoder()
 nd=be.fit_transform(df['Ord_2'])
 dfb=pd.concat([df,nd],axis=1)
 dfb
 
 from category_encoders import TargetEncoder
 te=TargetEncoder()
 CC=df.copy()
 new=te.fit_transform(X=CC["City"],y=CC["Target"])
 CC=pd.concat([CC,new],axis=1)
 CC


 import pandas as pd
 from scipy import stats
 import numpy as np
 df=pd.read_csv("/content/Data_to_Transform.csv")
 df



df.skew()

np.log(df["Highly Positive Skew"])

 np.reciprocal(df["Moderate Positive Skew"])


 np.sqrt(df["Highly Positive Skew"])


 df["Highly Positive Skew_boxcox"], parameters=stats.boxcox(df["Highly Positive Skew"])
 df

image
 df.skew()


df["Highly Negative Skew_yeojohnson"],parameters=stats.yeojohnson(df["Highly Negative Skew"])
df.skew()

from sklearn.preprocessing import QuantileTransformer
qt=QuantileTransformer(output_distribution='normal')
df["Moderate Negative Skew_1"]=qt.fit_transform(df[["Moderate Negative Skew"]])
df

import seaborn as sns
import statsmodels.api as sm # STATS MODEL- STATISTICAL MODEL TO VISUALIZE DISTRIBUTION
import matplotlib.pyplot as plt
sm.qqplot(df["Moderate Negative Skew"],line='45') # QQ - QUANTILE QUANTILE PLOT
plt.show()


sm.qqplot(np.reciprocal(df["Moderate Negative Skew"]),line='45') # RECIPROCAL
plt.show()

from sklearn.preprocessing import QuantileTransformer
qt=QuantileTransformer(output_distribution='normal',n_quantiles=891)
df["Moderate Negative Skew"]=qt.fit_transform(df[["Moderate Negative Skew"]])
sm.qqplot(df["Moderate Negative Skew"],line='45')
plt.show()
<img width="362" height="300" alt="593947601-00e4d3ca-f2b4-4f93-9244-73d7b32a427e" src="https://github.com/user-attachments/assets/248cea33-cad8-4fdd-b10e-1cbeb9450d06" />
<img width="352" height="152" alt="593947864-d3463172-b958-4e41-a004-6abaa1eb16d2" src="https://github.com/user-attachments/assets/eb269114-be32-4dff-9748-657d3f5c2bc2" />
<img width="486" height="305" alt="593948432-59ae3e3c-f3fa-4774-a9f1-04244b3fa83b" src="https://github.com/user-attachments/assets/a73dbab2-1e40-4fbc-92ce-b511d634f120" />
<img width="541" height="296" alt="593948513-3a09f990-a765-4ed9-970b-03f6cc697b93" src="https://github.com/user-attachments/assets/13904afa-d9d4-42db-8d4a-98094d988bc9" />
<img width="470" height="295" alt="593948741-e70f2a65-1256-4a3b-b7f0-f2d46be80ece" src="https://github.com/user-attachments/assets/233c4eae-7ce4-4ad2-8710-e05c0fae771b" />

<img width="545" height="305" alt="593948937-1673afdf-e0cf-4c71-a4a8-36733413cd15" src="https://github.com/user-attachments/assets/3a8bbaf8-99d6-49bf-aa41-d409b108664c" />
<img width="1061" height="282" alt="593949345-e5cea765-b171-401a-b8d5-9bdbc78ee64c" src="https://github.com/user-attachments/assets/44801f0f-fc9e-4a90-895f-d09d91bb9d75" />
<img width="415" height="286" alt="593949594-76ddf30e-3a9f-41d9-b115-c3ce50937486" src="https://github.com/user-attachments/assets/f5397222-b993-4134-825c-a228183f701e" />
<img width="586" height="298" alt="593950015-1942e4f6-1293-4727-9b4e-d5da199fed8d" src="https://github.com/user-attachments/assets/e876d8be-6029-4f74-91d1-751f600bb3ca" />
<img width="640" height="302" alt="593949825-71a40b11-c9f5-4af4-a91f-289d943ce0fd" src="https://github.com/user-attachments/assets/a56b6396-650b-4c94-bacf-f8605fb3bb70" />
<img width="730" height="350" alt="593950249-d034e217-b4d4-40f9-adbe-3368c0084b5b" src="https://github.com/user-attachments/assets/f049a504-d41f-4f85-af01-4363e0f7b9ba" />
<img width="378" height="145" alt="593950470-011159e4-63d8-4e3d-852b-21b3f760e8fd" src="https://github.com/user-attachments/assets/92763c84-2089-4372-be84-7e2525135052" />
<img width="287" height="363" alt="593950687-da9574c5-10fb-4c58-b862-b22f31514be4" src="https://github.com/user-attachments/assets/fd4ae4bc-7fdd-4657-a62f-c116ebbf7428" />
<img width="233" height="371" alt="593950924-595f3099-0338-4838-b520-8bfc42254f49" src="https://github.com/user-attachments/assets/7b9d5b03-9954-4b06-b7c6-362d2040a75f" />
<img width="206" height="368" alt="593951129-157b5c8a-7135-4fa8-99c6-aeae22ab52aa" src="https://github.com/user-attachments/assets/34160f52-3e79-43ad-af5f-de4e3ae105b6" />
<img width="802" height="372" alt="593951569-af047633-135d-4cfb-a1bd-62d1c20fecf1" src="https://github.com/user-attachments/assets/e65377ae-fbcd-4027-832e-d4cc39d44025" />
<img width="322" height="180" alt="593951743-f03ae772-4969-43d8-a82d-5931b714a2fe" src="https://github.com/user-attachments/assets/70bc2f07-43ed-4a1a-af6c-6d578a929689" />
<img width="302" height="206" alt="593952119-b0452924-930e-445c-849b-bc6c3c25548c" src="https://github.com/user-attachments/assets/9b2586f0-72cb-47dc-a1c6-b95bff29975f" />
<img width="810" height="377" alt="593952294-7ae6e544-4c0e-4143-abbc-98430e09cdfa" src="https://github.com/user-attachments/assets/6ef5cfcf-16fc-4602-b912-2dafe7a97bbf" />
<img width="553" height="357" alt="593952781-c0bd63eb-08e1-463b-b853-1e835021943a" src="https://github.com/user-attachments/assets/24b21aa5-f7f8-4309-a79a-8b21bd0d3f77" />
<img width="540" height="362" alt="593952504-c5fb8c36-e072-4078-a4ee-ce04ed4a1474" src="https://github.com/user-attachments/assets/1d0fb059-03a3-4480-a99b-aa1c16d2772f" />
<img width="556" height="371" alt="593953046-cc770c7b-cd82-4ba8-a816-0065bd86abbf" src="https://github.com/user-attachments/assets/2a8ff5a3-1e3d-4b55-b446-f9f92fa10a8b" />    # INCLUDE YOUR CODING AND OUTPUT SCREENSHOTS HERE
# RESULT:
       # INCLUDE YOUR RESULT HERE

       
