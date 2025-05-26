# Data-Analyst-data-
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

df = pd.read_csv('DataAnalyst.csv')
df

print("Dataset Shape:", df.shape)
print("\nFirst 5 rows:")
print(df.head())

print("\nData Types:")
print(df.dtypes)

print("\nMissing Values:")
print(df.isnull().sum())

print("\nSummary Statistics:")
print(df.describe(include='all'))

print(df.columns)

 if 'avg_salary' in df.columns:
        plt.figure(figsize=(10, 5))
        sns.histplot(df['avg_salary'].dropna(), bins=30, kde=True)
        plt.title("Distribution of Average Salaries")
        plt.xlabel("Average Salary (USD)")
        plt.ylabel("Number of Jobs")
        plt.tight_layout()
        plt.show()
    else:
        print("'avg_salary' column was not created.")


if 'avg_salary' in df.columns and 'Rating' in df.columns:
    plt.figure(figsize=(10, 5))
    sns.scatterplot(x='Rating', y='avg_salary', data=df)
    plt.title("Average Salary vs Company Rating")
    plt.xlabel("Company Rating")
    plt.ylabel("Average Salary (USD)")
    plt.tight_layout()
    plt.show()
else:
    print("Required columns 'avg_salary' or 'Rating' not found.")


    if 'avg_salary' in df.columns and 'Location' in df.columns:
    top_locations = df['Location'].value_counts().nlargest(10).index
    df_top_locations = df[df['Location'].isin(top_locations)]

    plt.figure(figsize=(12, 6))
    sns.boxplot(x='Location', y='avg_salary', data=df_top_locations)
    plt.title("Average Salary by Location (Top 10)")
    plt.xlabel("Location")
    plt.ylabel("Average Salary (USD)")
    plt.xticks(rotation=45)
    plt.tight_layout()
    plt.show()
else:
    print("Required columns 'avg_salary' or 'Location' not found.")



if 'avg_salary' in df.columns and 'Job Title' in df.columns:
    top_titles = df['Job Title'].value_counts().nlargest(10).index
    df_top_titles = df[df['Job Title'].isin(top_titles)]

    plt.figure(figsize=(12, 6))
    sns.boxplot(x='Job Title', y='avg_salary', data=df_top_titles)
    plt.title("Average Salary by Job Title (Top 10)")
    plt.xlabel("Job Title")
    plt.ylabel("Average Salary (USD)")
    plt.xticks(rotation=45, ha='right')
    plt.tight_layout()
    plt.show()
else:
    print("Required columns 'avg_salary' or 'Job Title' not found.")


if 'avg_salary' in df.columns and 'Size' in df.columns:
    plt.figure(figsize=(12, 6))
    sns.boxplot(x='Size', y='avg_salary', data=df)
    plt.title("Average Salary by Company Size")
    plt.xlabel("Company Size")
    plt.ylabel("Average Salary (USD)")
    plt.xticks(rotation=45)
    plt.tight_layout()
    plt.show()
else:
    print("Required columns 'avg_salary' or 'Size' not found.")    


if 'avg_salary' in df.columns and 'Type of ownership' in df.columns:
    plt.figure(figsize=(12, 6))
    sns.boxplot(x='Type of ownership', y='avg_salary', data=df)
    plt.title("Average Salary by Type of Ownership")
    plt.xlabel("Type of Ownership")
    plt.ylabel("Average Salary (USD)")
    plt.xticks(rotation=45, ha='right')
    plt.tight_layout()
    plt.show()
else:
    print("Required columns 'avg_salary' or 'Type of ownership' not found.")

if 'avg_salary' in df.columns and 'Industry' in df.columns:
    top_industries = df['Industry'].value_counts().nlargest(10).index
    df_top_industries = df[df['Industry'].isin(top_industries)]

    plt.figure(figsize=(12, 6))
    sns.boxplot(x='Industry', y='avg_salary', data=df_top_industries)
    plt.title("Average Salary by Industry (Top 10)")
    plt.xlabel("Industry")
    plt.ylabel("Average Salary (USD)")
    plt.xticks(rotation=45, ha='right')
    plt.tight_layout()
    plt.show()
else:
    print("Required columns 'avg_salary' or 'Industry' not found.")

if 'avg_salary' in df.columns and 'Competitors' in df.columns:
    df['Has_Competitors'] = df['Competitors'].apply(lambda x: 'Yes' if isinstance(x, str) and x != '-1' else 'No')
    
    plt.figure(figsize=(8, 5))
    sns.boxplot(x='Has_Competitors', y='avg_salary', data=df)
    plt.title("Salary Distribution by Presence of Competitor Info")
    plt.xlabel("Has Competitor Info")
    plt.ylabel("Average Salary (USD)")
    plt.tight_layout()
    plt.show()
else:
    print("Required columns 'avg_salary' or 'Competitors' not found.")


 if 'avg_salary' in df.columns and 'Job Description' in df.columns:
    df['desc_length'] = df['Job Description'].apply(lambda x: len(str(x).split()))
    
    plt.figure(figsize=(10, 5))
    sns.scatterplot(x='desc_length', y='avg_salary', data=df)
    plt.title("Salary vs. Job Description Length")
    plt.xlabel("Job Description Word Count")
    plt.ylabel("Average Salary (USD)")
    plt.tight_layout()
    plt.show()
else:
    print("Required columns 'avg_salary' or 'Job Description' not found.")

if 'Location' in df.columns:
    print("\nTop 10 Job Locations:")
    print(df['Location'].value_counts().head(10))
else:
    print("'Location' column not found.")


if 'Job Title' in df.columns:
    print("\nTop 10 Job Titles:")
    print(df['Job Title'].value_counts().head(10))
else:
    print("'Job Title' column not found.")

if 'Company Name' in df.columns:
    print("\nTop 10 Companies by Job Postings:")
    print(df['Company Name'].value_counts().head(10))
else:
    print("'Company Name' column not found.")


if 'avg_salary' in df.columns and 'Job Title' in df.columns:
    top_titles = df['Job Title'].value_counts().nlargest(10).index
    avg_salary_by_title = df[df['Job Title'].isin(top_titles)].groupby('Job Title')['avg_salary'].mean().sort_values(ascending=False)
    print("\nAverage Salary for Top 10 Job Titles:")
    print(avg_salary_by_title)
else:
    print("'avg_salary' or 'Job Title' column not found.")


        if 'avg_salary' in df.columns and 'Rating' in df.columns:
    df['Rating_bin'] = pd.cut(df['Rating'], bins=[0, 2, 3, 4, 5], labels=['0-2', '2-3', '3-4', '4-5'])
    print("\nAverage Salary by Company Rating Bin:")
    print(df.groupby('Rating_bin')['avg_salary'].mean())
else:
    print("'avg_salary' or 'Rating' column not found.")
    

  if 'avg_salary' in df.columns and 'Competitors' in df.columns:
    df['Has_Competitors'] = df['Competitors'].apply(lambda x: 'Yes' if isinstance(x, str) and x != '-1' else 'No')
    print("\nAverage Salary Based on Competitor Info:")
    print(df.groupby('Has_Competitors')['avg_salary'].mean())
else:
    print("'avg_salary' or 'Competitors' column not found.")



 if 'Job Description' in df.columns:
    df['desc_length'] = df['Job Description'].apply(lambda x: len(str(x).split()))
    print("\nJob Description Length Stats (in words):")
    print(df['desc_length'].describe())
else:
    print("'Job Description' column not found.")


print("DataFrame Shape:", df.shape)
print("\nColumn Names:\n", df.columns.tolist())
print("\nData Types:\n", df.dtypes)
print("\nMissing Values:\n", df.isnull().sum())


if 'avg_salary' in df.columns:
    print("\nSalary Summary Statistics:")
    print(df['avg_salary'].describe())
else:
    print("'avg_salary' column not found.")
   


   
    
