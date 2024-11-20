# **Income Analysis of 30K USA Citizens**  

## 🗂️ **About the Dataset**  
This dataset provides detailed information about 30,000 American citizens, including:  
- **Income range**  
- **Age**  
- **Education level**  
- And more demographic details.  

The dataset is versatile and can be used for a variety of tasks:  
- Classification  
- Data Analytics  
- Statistical Analysis  

---

## 🛠️ **Project Overview**  
In this project, I conducted an in-depth analysis of the dataset using:  
1. **Exploratory Data Analysis (EDA)**:
```python


Categorical_Analysis_columns = ["Job","Education","Marital_Status","Relationship","Race","Gender"]

for i in range(len(Categorical_Analysis_columns)):
    for f in range(len(Categorical_Analysis_columns)-1):
        if i != f+1:
            Categorical_Analysis_columns_visualization = pd.crosstab(df[Categorical_Analysis_columns[i]],df[Categorical_Analysis_columns[f+1]])
            
            # In This I performed the crosstab among all the Categorical-Categorical columns 
            print(Categorical_Analysis_columns_visualization)
            
            # In this I create the stacked bar among them 
            Categorical_Analysis_columns_visualization.plot(kind="bar",stacked=True)

   ```
![Income Analysis](https://github.com/Arif-miad/Income-Analysis-of-30K-USA-Citizens/blob/main/Arif4.png)
```python
bigfig = plt.figure(figsize=(12,6))

(top,central,bottom) = bigfig.subfigures(3,1)

### Top figures ###
top.subplots_adjust(left=.1,right=.9,wspace=.4,hspace=.4)

fig,(ax1,ax2,ax3) = plt.subplots(ncols=3,figsize=(12,6))

ax1 = sns.histplot(data=df,x='Sex',ax=ax1)
ax1.set_title('Sex of the Person',size=16)

result = df.loc[df.Workclass != ' ?'].groupby('Workclass')['Workclass'].count().reset_index(name='Count').sort_values('Count',ascending=False)
ax2 = sns.barplot(data=result.loc[result.Count > 50],x='Workclass',y='Count',ax=ax2)
ax2.set_xticklabels(ax2.get_xticklabels(),rotation=45,fontsize=10)
ax2.set_title('Workclass of the Person',size=16)

ax3 = sns.histplot(data=df,x='Age',bins=10,ax=ax3)
ax3.set_title('Age of the Person',size=16)

plt.tight_layout()

### Central figures ###
central.subplots_adjust(left=.1,right=.9,wspace=.4,hspace=.4)

fig,(ax1,ax2,ax3) = plt.subplots(ncols=3,figsize=(12,6))

result = df.groupby('Race')['Race'].count().reset_index(name='Count').sort_values('Count',ascending=False)
ax1 = sns.barplot(data=result,x='Race',y='Count',ax=ax1)
ax1.set_xticklabels(ax1.get_xticklabels(),rotation=45,fontsize=8)
ax1.set_title('Race of the Person',size=16)

result = df.loc[df['Native-country'] != ' ?'].groupby('Native-country')['Native-country'].count().reset_index(name='Count').sort_values('Count',ascending=False).head(6)
ax2 = sns.barplot(data=result,x='Native-country',y='Count',ax=ax2)
ax2.set_xticklabels(ax2.get_xticklabels(),rotation=45,fontsize=8)
ax2.set_yscale("log")
ax2.set_title('Native Country of the Person',size=16)

ax3 = sns.histplot(data=df,x='Income',ax=ax3)
ax3.set_title('Income of the Person',size=16)

plt.tight_layout()

### Bottom figures ###
bottom.subplots_adjust(left=.1,right=.9,wspace=.4,hspace=.4)

fig,(ax1,ax2,ax3) = plt.subplots(ncols=3,figsize=(12,6))

result = df.groupby('Education')['Education'].count().reset_index(name='Count').sort_values('Count',ascending=False)
ax1 = sns.barplot(data=result,x='Education',y='Count',ax=ax1)
ax1.set_xticklabels(ax1.get_xticklabels(),rotation=65,fontsize=8)
ax1.set_title('Education Level of the Person',size=16)

result = df.groupby('Marital-status')['Marital-status'].count().reset_index(name='Count').sort_values('Count',ascending=False)
ax2 = sns.barplot(data=result.loc[result.Count > 50],x='Marital-status',y='Count',ax=ax2)
ax2.set_xticklabels(ax2.get_xticklabels(),rotation=50,fontsize=8)
ax2.set_title('Marital Status of the Person',size=16)

result = df.groupby('Occupation')['Occupation'].count().reset_index(name='Count').sort_values('Count',ascending=False)
ax3 = sns.barplot(data=result.loc[result.Count > 50],x='Occupation',y='Count',ax=ax3)
ax3.set_xticklabels(ax3.get_xticklabels(),rotation=75,fontsize=8)
ax3.set_title('Occupation of the Person',size=16)

plt.tight_layout()

plt.show()
```
![Dataset Overview](https://github.com/Arif-miad/Income-Analysis-of-30K-USA-Citizens/blob/main/Arif6.png)

```python
for col in columns:
    data = df[df[col] != ' ?']


bigfig = plt.figure(figsize=(12,6))

(top,bottom) = bigfig.subfigures(2,1)

### Top figures ###
top.subplots_adjust(left=.1,right=.9,wspace=.4,hspace=.4)

fig,(ax1,ax2) = plt.subplots(ncols=2,figsize=(12,5))

ax1 = sns.histplot(data=df,x='Income',hue='Sex',multiple='dodge',shrink=.7,ax=ax1)
ax1.set_title('Income vs Sex',size=18)

ax2 = sns.histplot(data=df,x='Income',hue='Marital-status',multiple='dodge',shrink=.7,ax=ax2)
ax2.set_title('Income vs Marital Status',size=18)
plt.setp(ax2.get_legend().get_texts(),fontsize='8') 

plt.tight_layout()

### Bottom figures ###
top.subplots_adjust(left=.1,right=.9,wspace=.4,hspace=.4)

fig,(ax1,ax2) = plt.subplots(ncols=2,figsize=(12,5))

ax1 = sns.histplot(data=df,x='Income',hue='Relationship',multiple='dodge',shrink=.7,ax=ax1)
ax1.set_title('Income vs Relationship Status',size=18)

ax2 = sns.histplot(data=df,x='Income',hue='Occupation',multiple='dodge',shrink=.7,ax=ax2)
ax2.set_title('Income vs Occupation',size=18)
plt.setp(ax2.get_legend().get_texts(),fontsize='7') 

plt.tight_layout()
```
![Dataset overview](https://github.com/Arif-miad/Income-Analysis-of-30K-USA-Citizens/blob/main/Arif7.png).
![Dataset Overview](https://github.com/Arif-miad/Income-Analysis-of-30K-USA-Citizens/blob/main/Arif8.png)




   - Identified patterns and trends in the data.  
   - Visualized relationships between key features like age, education, and income.  

3. **Data Preprocessing**:  
   - Handled missing values and outliers.  
   - Scaled numerical features for better model performance.  
   - Encoded categorical variables for machine learning algorithms.  

4. **Machine Learning Implementation**:  
   - Utilized multiple algorithms, including **Gradient Boosting**, to predict income levels.  
   - Experimented with hybrid models to enhance prediction accuracy.  

---

## 🔧 **Tools and Techniques**  
- **Python Libraries**:  
  - Pandas, NumPy, Matplotlib, Seaborn for EDA.  
  - Scikit-learn for preprocessing and modeling.  
  - Gradient Boosting models for classification tasks.  
- **Evaluation Metrics**:  
  - Accuracy, Precision, Recall, ROC-AUC Curve.  

---

## 📈 **Results**  
The hybrid approach demonstrated significant improvements in model accuracy and performance. Key insights were derived from feature importance and EDA visualizations.  

---

## 🔗 **Links to My Work**  
- 📘 **Kaggle Notebook**: [https://www.kaggle.com/arifmia](#)  
- 💼 **LinkedIn Profile**: [www.linkedin.com/in/arif-miah-8751bb217](#)  

