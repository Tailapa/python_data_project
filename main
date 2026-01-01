import pandas as pd
import matplotlib.pyplot as plt

# 1. Load the data from the 'data' subfolder
# We use the relative path 'data/filename.csv'
file_path = 'data/suicides_profession_wise.csv'
df = pd.read_csv(file_path)

# Step 1: Geometry Cleaning
# We remove 'Total' rows to ensure we are only looking at individual States/UTs
df_clean = df[~df['State/UT'].str.contains('Total', na=False)]

# --- QUESTION 1: National Profession Distribution ---
prof_cols = {
    'House wives': 'House wife - Total',
    'Professionals': 'Professionals/Salaried Persons (Total) - Total',
    'Students': 'Students - Total',
    'Unemployed': 'Unemployed Persons - Total',
    'Self-employed': 'Self-employed Persons(Total) - Total',
    'Farming Sector': 'Persons Engaged in Farming Sector (Total) - Total',
    'Daily Wage Earner': 'Daily Wage Earner - Total'
}

prof_totals = {label: df_clean[col].sum() for label, col in prof_cols.items()}
prof_df = pd.DataFrame(list(prof_totals.items()), columns=['Profession', 'Total']).sort_values(by='Total')

# Plot 1: Profession Horizontal Bar
plt.figure(figsize=(10, 6))
plt.barh(prof_df['Profession'], prof_df['Total'], color='#2c3e50')
plt.title('Suicides by Profession (National Distribution)')
plt.xlabel('Total Count')
plt.tight_layout()
plt.savefig('profession_distribution.png')

# --- QUESTION 2: Top 10 States for Student Suicides ---
student_data = df_clean[['State/UT', 'Students - Total']].sort_values(by='Students - Total', ascending=False).head(10)

# Plot 2: Student Suicides by State
plt.figure(figsize=(10, 6))
plt.bar(student_data['State/UT'], student_data['Students - Total'], color='#e67e22')
plt.title('Top 10 States: Student Suicides')
plt.xticks(rotation=45)
plt.ylabel('Count')
plt.tight_layout()
plt.savefig('student_suicides_by_state.png')

# --- QUESTION 3: Gender Breakdown (Daily Wage vs House wives) ---
comparison = pd.DataFrame({
    'Category': ['Daily Wage Earner', 'House wife'],
    'Male': [df_clean['Daily Wage Earner - Male'].sum(), df_clean['House wife - Male'].sum()],
    'Female': [df_clean['Daily Wage Earner - Female'].sum(), df_clean['House wife - Female'].sum()]
})

# Plot 3: Gender Comparison Stacked Bar
comparison.set_index('Category').plot(kind='bar', stacked=True, color=['#3498db', '#e91e63'], figsize=(8, 6))
plt.title('Gender Dynamics: Labor vs. Domestic Spheres')
plt.ylabel('Count')
plt.xticks(rotation=0)
plt.tight_layout()
plt.savefig('gender_comparison.png')

print("Analysis complete. Check your folder for the PNG plots!")